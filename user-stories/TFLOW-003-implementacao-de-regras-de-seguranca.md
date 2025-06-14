### **Estória de Usuário: Implementação de Regras de Segurança**

**ID da Estória:** TFLOW-003 

**Feature:** Infraestrutura e Segurança 

**Pontos de Estória (Estimativa):** 5

- **Como um:** Desenvolvedor(a) da equipe de infraestrutura.
- **Eu quero:** Escrever e implantar um conjunto completo de Regras de Segurança no Firestore.
- **Para que:** A integridade e a privacidade dos dados da aplicação sejam garantidas no nível do servidor, prevenindo acessos não autorizados e modificações indevidas.

#### **Critérios de Aceitação (AC)**

1. **Regras de Perfil (`users`):** Um usuário só pode ler seu próprio documento e o de outros (para fins de exibição), mas só pode **escrever** em seu próprio documento. A alteração do campo `role` deve ser bloqueada para todos, exceto administradores.
2. **Regras de Currículo (`resumes`):** Um usuário só pode ler e escrever em seu próprio documento de currículo.
3. **Regras de Vagas (`vacancies`):** Qualquer pessoa (autenticada ou não) pode ler as vagas com `status: 'Aberta'`. Apenas usuários com `role` de `recruiter` ou `admin` podem criar ou modificar vagas.
4. **Regras de Curadoria (`technologies`, etc.):** Apenas usuários com `role` de `admin` podem escrever nestas coleções.
5. **Implantação:** As regras devem ser escritas no arquivo `firestore.rules` e implantadas no ambiente Firebase.