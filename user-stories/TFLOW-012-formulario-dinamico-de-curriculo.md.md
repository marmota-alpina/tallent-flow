# Estória de Usuário: Construção do Formulário Dinâmico de Cadastro de Currículo

**ID da Estória:** TFLOW-012
**Feature:** Perfil do Candidato

* **Como um:** Candidato logado no sistema Tallent Flow.
* **Eu quero:** Preencher meu currículo de forma guiada e dinâmica, adicionando minhas informações de contato, foco profissional, formação, idiomas e experiências detalhadas, incluindo os problemas que resolvi e as tecnologias e soft skills que utilizei.
* **Para que:** Eu possa criar um perfil profissional completo e detalhado, que aumente minhas chances de ser encontrado por recrutadores e me destaque no processo seletivo.

### Critérios de Aceitação (AC)

1.  **Estrutura de Wizard:** O formulário deve ser dividido em etapas com uma barra de progresso (Contato, Foco, Formação, Idiomas, Experiências).
2.  **Campos Dinâmicos:** As seções de Formação, Idiomas e Experiências Profissionais devem permitir ao usuário adicionar múltiplos blocos de informação dinamicamente.
3.  **Lógica Condicional:**
    * O campo "Data de Término" em uma experiência deve ser desabilitado se o toggle "Trabalho atual" estiver ativo.
    * O select de "Tecnologia Específica" deve ter suas opções filtradas com base no valor do select "Tipo de Tecnologia" (select em cascata).
4.  **Consumo de Dados da Curadoria:** Todos os campos `select` (Área de Atuação, Tecnologias, Soft Skills, etc.) devem ser populados com os dados gerenciados na Área de Curadoria (TFLOW-011).
5.  **Submissão e Persistência:** Ao final, o formulário completo deve ser salvo como um único documento na coleção `resumes` do Firestore, associado ao ID do usuário.
6.  **Responsividade:** O formulário deve ser totalmente funcional e visualmente agradável em dispositivos móveis e desktops.