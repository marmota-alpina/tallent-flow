# Estória de Usuário: Construção do Formulário Dinâmico de Cadastro de Currículo

**ID da Estória:** TFLOW-012
**Feature:** Perfil do Candidato
**Pontos de Estória (Estimativa):** 13

- **Como um:** Candidato logado no sistema Tallent Flow.
- **Eu quero:** Preencher meu currículo de forma guiada e dinâmica.
- **Para que:** Eu possa criar um perfil profissional completo e detalhado.

## Critérios de Aceitação (AC)

1.  **Estrutura de Wizard:** O formulário deve ser dividido em etapas com uma barra de progresso.
2.  **Campos Dinâmicos:** As seções de Formação, Idiomas e Experiências Profissionais devem permitir ao usuário adicionar múltiplos blocos de informação.
3.  **Lógica Condicional:** Lógica de toggle para "Trabalho atual" e selects em cascata para tecnologias.
4.  **Consumo de Dados da Curadoria:** Todos os campos `select` devem ser populados com os dados da Área de Curadoria.
5.  **Submissão e Persistência:** Ao final, o formulário completo deve ser salvo como um único documento na coleção `resumes`.
6.  **Responsividade:** O formulário deve ser totalmente funcional e visualmente agradável em dispositivos móveis e desktops.
7.  **Submissão e Persistência de Dados (AC7):**
    -   Ao clicar em "Finalizar" na última etapa, o objeto completo do formulário deve ser validado.
    -   Em caso de sucesso, o objeto JSON do currículo é salvo na coleção `resumes` do Firestore, com o documentId sendo o `userId` do usuário logado.
    -   **O documento salvo deve incluir um novo campo `status: "draft"` para indicar que ele foi salvo, mas ainda não foi publicado pelo usuário.**
    -   O sistema deve fornecer feedback visual de sucesso (ex: "Rascunho do currículo salvo com sucesso!").