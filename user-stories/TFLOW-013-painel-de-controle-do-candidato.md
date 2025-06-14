### **Estória de Usuário: Painel de Controle do Candidato**

**ID da Estória:** TFLOW-013

**Feature:** Experiência do Candidato 

**Pontos de Estória (Estimativa):** 5

- **Como um:** Candidato que já preencheu e salvou seu currículo.
- **Eu quero:** Acessar uma página de painel de controle ("dashboard") que mostre o status do meu perfil e as oportunidades que o sistema encontrou para mim.
- **Para que:** Eu possa acompanhar o progresso da minha candidatura, manter meu currículo atualizado e me engajar com as vagas mais relevantes para meu perfil.

#### **Critérios de Aceitação (AC)**

1. **Rota e Acesso:** Deve ser criada uma rota protegida `/meu-painel`, que se tornará a página principal para um candidato após o login.
2. **Status do Perfil:** A página deve exibir de forma clara o status da análise de IA do perfil do usuário, lendo o campo `iaClassification.status` do seu documento no Firestore (ex: "Análise Pendente", "Perfil Analisado com Sucesso").
3. **Resumo do Perfil:** Um pequeno card ou seção deve exibir um resumo do perfil do candidato (ex: "Desenvolvedor Pleno, especialista em Angular e Node.js").
4. **Vagas Recomendadas:** A página deve conter uma seção que lista as vagas para as quais o sistema de IA encontrou uma alta compatibilidade.
5. **Ações Rápidas:** A página deve conter botões ou links claros para as ações mais comuns, como "Editar meu Currículo".