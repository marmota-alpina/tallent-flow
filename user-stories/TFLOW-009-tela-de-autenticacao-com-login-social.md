### **Estória de Usuário: Tela de Autenticação com Login Social**

**ID da Estória:** TFLOW-009 **Feature:** Autenticação de Usuários **Pontos de Estória (Estimativa):** 5

- **Como um:** Visitante não autenticado da plataforma Talent Flow.
- **Eu quero:** Acessar uma página de login clara e simples onde eu possa me autenticar na plataforma usando minha conta do Google.
- **Para que:** Eu possa acessar de forma rápida e segura os recursos protegidos do Talent Flow, como meu painel de candidato ou a área de administração.

### **Critérios de Aceitação (AC)**

#### **AC1: Acesso e Roteamento**

- Deve existir uma rota pública em `/login` que renderize o componente `LoginComponent`.
- Qualquer tentativa de acesso a uma rota protegida (ex: `/curation`, `/meu-curriculo`) por um usuário não autenticado deve ser interceptada pelo `auth.guard` e redirecionada automaticamente para a página `/login`.
- Se um usuário já autenticado tentar acessar a página `/login`, ele deve ser redirecionado para a página principal de seu perfil (ex: dashboard do candidato).

#### **AC2: Design e Interface da Tela de Login**

- A tela deve ser minimalista, com os elementos centralizados para focar a atenção do usuário na ação de login.
- O logo do "Talent Flow" deve ser exibido com destaque no topo da tela.
- Deve haver um texto de chamada para ação claro e conciso, como "Bem-vindo! Acesse a plataforma para decolar sua carreira."
- O único método de autenticação visível deve ser um botão proeminente com o texto **"Entrar com o Google"**, acompanhado do logo oficial do Google para gerar confiança.
- Todo o design da página (cores, fontes, espaçamentos) deve seguir estritamente o Sistema de Design definido na **ADR-010**.

#### **AC3: Fluxo de Autenticação (Caminho Feliz)**

- Ao clicar no botão "Entrar com o Google", o método `loginWithGoogle()` do `AuthService` deve ser invocado.
- O fluxo de autenticação do Firebase com o provedor Google deve ser iniciado, abrindo um popup para o usuário selecionar sua conta.
- Após a autenticação bem-sucedida no popup do Google, ele deve ser fechado.
- A aplicação deve redirecionar o usuário para a rota apropriada pós-login (a rota que ele tentou acessar originalmente ou uma rota padrão de dashboard).

#### **AC4: Tratamento de Cancelamento e Erros**

- Se o usuário fechar o popup do Google sem se autenticar, ele deve permanecer na tela de login sem que nenhum erro seja exibido.
- Se ocorrer um erro durante o processo de autenticação com o Firebase (ex: problema de rede, conta bloqueada pelo provedor), uma notificação de erro amigável (um "toast") deve ser exibida ao usuário, informando sobre a falha. O usuário deve permanecer na tela de login.

#### **AC5: Responsividade**

- O layout da tela de login deve ser totalmente responsivo, garantindo uma experiência de usuário perfeita em dispositivos móveis, tablets e desktops. Os elementos devem se reajustar de forma fluida e manter a clareza em qualquer tamanho de tela.