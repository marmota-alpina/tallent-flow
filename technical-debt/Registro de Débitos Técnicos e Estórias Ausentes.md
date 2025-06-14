## **Documento: Registro de Débitos Técnicos e Estórias Ausentes**

**Data:** 14 de junho de 2025

**Status:** Proposto

#### **1. Contexto**

Durante a revisão da arquitetura e das estórias de usuário existentes, foram identificados alguns requisitos técnicos e de infraestrutura que são cruciais para a estabilidade, segurança e eficiência do ecossistema Talent Flow.

Embora não representem funcionalidades diretas para o usuário final, essas tarefas são fundamentais para sustentar a arquitetura Poly-Repo decidida no **ADR 015** e garantir a resiliência do sistema. Este documento formaliza esses itens como "débitos" a serem planejados, para que possam ser priorizados e incluídos no backlog de desenvolvimento.

#### **2. Débitos Identificados**

##### **Débito 1: Pacote de Tipos Compartilhados para Arquitetura Poly-Repo**

- **ID da Estória (Proposto):** `TFLOW-005`
    
- **Feature:** Infraestrutura e Qualidade de Código
    
- **Título:** Criação e Publicação do Pacote NPM Privado `talent-flow-shared-types`
    
- **Descrição:** O **ADR 015** define uma arquitetura Poly-Repo onde o frontend (`talent-flow-webapp`), as Cloud Functions (`talent-flow-functions`) e outros possíveis serviços TypeScript precisam compartilhar as mesmas interfaces de dados (ex: `UserProfile`, `Vacancy`, `Resume`). A decisão especifica que esse compartilhamento será feito via um pacote NPM privado. Atualmente, não há uma estória para criar, gerenciar e publicar este pacote essencial.
    
- **Riscos da Não-Implementação:**
    
    - Duplicação manual de interfaces entre os repositórios, levando a inconsistências.
    - Erros de integração difíceis de depurar quando um serviço espera um formato de dados diferente do que o outro envia.
    - Violação da estratégia de compartilhamento de código definida na arquitetura.
- **Critérios de Aceitação Sugeridos:**
    
    1. Deve ser criado um novo repositório Git (`talent-flow-shared-types`).
    2. As interfaces e modelos de dados principais (`UserProfile`, `Vacancy`, etc.) devem ser definidos neste repositório.
    3. O projeto deve ser configurado como um pacote NPM, com um `package.json` adequado.
    4. Um pipeline de CI/CD (ex: GitHub Actions) deve ser criado para publicar automaticamente uma nova versão do pacote em um registro privado (ex: GitHub Packages) a cada merge na branch principal.
    5. Os projetos `talent-flow-webapp` e `talent-flow-functions` devem ser atualizados para remover as definições de tipo locais e consumir este pacote como uma dependência.

---

##### **Débito 2: Pipeline de Integração e Deploy Contínuo (CI/CD)**

- **ID da Estória (Proposto):** `TFLOW-004` (conforme mencionado no `README.md`)
    
- **Feature:** Infraestrutura de DevOps
    
- **Título:** Configuração do Pipeline de CI/CD para os Repositórios do Ecossistema
    
- **Descrição:** O `README.md` recomenda a criação de uma estória para o pipeline de CI/CD, mas o arquivo correspondente não existe. Em uma arquitetura com múltiplos repositórios, a automação de testes e deploys é crucial para manter a agilidade e reduzir o risco de erros manuais.
    
- **Riscos da Não-Implementação:**
    
    - Processos de deploy manuais, lentos e propensos a falhas.
    - Falta de padronização de qualidade (lint, testes) antes do deploy.
    - Dificuldade em manter a consistência entre os ambientes de desenvolvimento, staging e produção.
- **Critérios de Aceitação Sugeridos:**
    
    1. Deve ser criado um workflow de CI/CD para o repositório `talent-flow-webapp` que execute lint, testes, build e deploy para o ambiente de destino (ex: Cloud Run/Firebase Hosting).
    2. Deve ser criado um workflow de CI/CD para o repositório `talent-flow-functions` que execute lint, testes e deploy para o Google Cloud Functions.
    3. Deve ser criado um workflow de CI/CD para o repositório `talent-flow-ia-api` que execute lint, testes, build da imagem Docker e deploy para o Google Cloud Run.
    4. Os pipelines devem ser acionados automaticamente em eventos de merge para a branch principal.

---

##### **Débito 3: Tratamento de Falhas na Fila de Mensagens (Dead-Letter Queue)**

- **ID da Estória (Proposto):** `TFLOW-022`
    
- **Feature:** Backend de Orquestração
    
- **Título:** Implementação de Dead-Letter Queue para o Tópico de Análise de Currículos
    
- **Descrição:** A comunicação entre as Cloud Functions e a API de IA é desacoplada via Google Cloud Pub/Sub, conforme o **ADR 0005**. Esta abordagem aumenta a resiliência, mas o fluxo atual (`TFLOW-020` e `TFLOW-021`) não especifica o que acontece se uma mensagem falhar no processamento repetidamente. Sem uma estratégia de "fila de mensagens mortas" (Dead-Letter Queue), essas mensagens podem ser descartadas permanentemente.
    
- **Riscos da Não-Implementação:**
    
    - Perda silenciosa de solicitações de análise de currículo, resultando em um perfil de candidato que nunca é analisado.
    - Falta de visibilidade sobre falhas de processamento na API de IA.
    - Experiência de usuário ruim, pois a plataforma não cumpre a promessa de analisar o perfil.
- **Critérios de Aceitação Sugeridos:**
    
    1. Um novo tópico Pub/Sub deve ser criado para servir como Dead-Letter Topic (DLT).
    2. A assinatura do Pub/Sub usada pela `talent-flow-ia-api` deve ser configurada para encaminhar mensagens para o DLT após um número definido de tentativas de entrega falhas.
    3. Deve ser configurado um sistema de alerta (ex: Cloud Monitoring) que notifique a equipe de desenvolvimento sempre que uma nova mensagem for enviada para o DLT.
    4. A documentação do backend deve ser atualizada com instruções sobre como inspecionar e, se possível, reprocessar as mensagens da DLT.