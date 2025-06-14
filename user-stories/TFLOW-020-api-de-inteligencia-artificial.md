# Estória de Usuário: API de Inteligência Artificial


**ID da Estória:** TFLOW-020

**Feature:** Backend de Análise de IA 

**Pontos de Estória (Estimativa):** 13

- **Como um:** Desenvolvedor(a) de Backend/IA.
- **Eu quero:** Criar e implantar um serviço FastAPI em Python no Cloud Run que possa processar dados de currículos e vagas de forma assíncrona.
- **Para que:** A plataforma possa oferecer os diferenciais de classificação de senioridade e matching automático entre candidatos e vagas.

#### **Critérios de Aceitação (AC)**

1. **Repositório e Setup:** Deve ser criado um novo repositório Git (`talent-flow-ia-api`) e um projeto FastAPI básico, conteinerizado com um `Dockerfile`.
2. **Consumo de Mensagens:** A API deve ser configurada para "escutar" um tópico do Google Cloud Pub/Sub e consumir as mensagens com dados de currículos enviadas para análise.
3. **Endpoint de Classificação:** Deve ser implementado um endpoint (`POST /classify-profile`) que:
    - Recebe o payload de um currículo.
    - Aplica uma lógica de análise inicial (para o MVP, pode ser baseada em regras, como anos de experiência e contagem de tecnologias-chave).
    - Atualiza o documento do usuário no Firestore com o resultado da classificação (ex: `{ iaClassification: { status: 'completed', level: 'Pleno', ... } }`).
4. **Endpoint de Matching:** Deve ser implementado um endpoint (`POST /match-vacancy`) que, ao receber os dados de uma nova vaga, busca candidatos qualificados no Firestore e aciona a função de notificação para aqueles com alta compatibilidade.
5. **Deploy:** A aplicação Dockerizada deve ser implantada com sucesso no Google Cloud Run e integrada ao Pub/Sub.