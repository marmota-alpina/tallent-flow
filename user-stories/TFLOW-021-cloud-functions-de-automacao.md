### **Estória de Usuário: Cloud Functions de Automação**

**ID da Estória:** TFLOW-021 

**Feature:** Backend de Orquestração 

**Pontos de Estória (Estimativa):** 8

- **Como um:** Desenvolvedor(a) de Backend.
- **Eu quero:** Criar e implantar as Cloud Functions que servem como a "cola" do sistema, conectando as diferentes partes de forma assíncrona.
- **Para que:** Possamos garantir que o sistema seja resiliente, desacoplado e que processos demorados não afetem a experiência do usuário na aplicação principal.

#### **Critérios de Aceitação (AC)**

1. **Repositório e Setup:** Deve ser criado um novo repositório Git (`talent-flow-functions`) e um projeto Firebase Functions com TypeScript.
2. **Função "Publicador":** Deve ser criada uma Cloud Function acionada pelo evento `onUpdate` da coleção `resumes` no Firestore. Ao detectar a atualização de um currículo, esta função deve pegar os dados relevantes e publicá-los em um tópico do Pub/Sub para serem consumidos pela API de IA.
3. **Função "Notificador":** Deve ser criada uma Cloud Function acionada por HTTP. Ela receberá uma lista de IDs de usuários e informações de uma vaga, e será responsável por enviar um e-mail formatado para cada um deles, informando sobre a oportunidade.
4. **Contratos de Dados:** Os formatos (schemas) das mensagens do Pub/Sub e dos payloads de notificação devem ser claramente definidos e documentados.