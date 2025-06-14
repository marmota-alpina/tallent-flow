# **Estória de Usuário: Implementação dos Padrões de Abstração**

ID da Estória: TFLOW-002

Feature: Arquitetura e Qualidade de Código

Pontos de Estória (Estimativa): 8

- **Como um:** Desenvolvedor(a) da equipe Talent Flow.
- **Eu quero:** Implementar um conjunto de componentes e classes base reutilizáveis para as funcionalidades de CRUD (Criar, Ler, Atualizar, Excluir) que serão usadas em toda a aplicação.
- **Para que:** Possamos acelerar o desenvolvimento de todas as páginas de gerenciamento (como Tecnologias, Cargos, Habilidades, etc.), garantindo consistência visual e de comportamento, e minimizando a duplicação de código desde o início do projeto.

### **Critérios de Aceitação (AC)**

#### **AC1: Implementação dos Serviços Base e Core**

- Deve ser criada uma classe abstrata `BaseCurationService` no diretório `src/app/core/services/`.
- Esta classe base deve conter a lógica genérica para interagir com o Firestore: `getCollection()`, `addItem(item)`, `updateItem(id, item)` e `deleteItem(id)` (implementando soft delete, ou seja, atualizando um campo `isActive: false`).
- Fica estabelecido que todos os serviços singleton da aplicação (como `AuthService`, `BreadcrumbService`, etc.) serão criados e mantidos dentro do diretório `src/app/core/services/`.

#### **AC2: Implementação do Componente Base de Curadoria**

- Deve ser criada uma classe abstrata `BaseCurationComponent`.
- Esta classe deve gerenciar o estado comum a todas as páginas de CRUD usando Angular Signals (ex: `items = signal([])`, `isLoading = signal(false)`, `showModal = signal(false)`).
- Deve conter os métodos genéricos para interagir com o serviço base (ex: `loadItems()`, `onEdit()`, `onDelete()`, `openModal()`), que serão herdados pelos componentes filhos.

#### **AC3: Criação dos Componentes de UI Reutilizáveis**

- Um componente `CurationTableComponent` deve ser criado no diretório `src/app/shared/components/`.
    - Ele deve ser um componente "burro" (presentational), recebendo a lista de itens via `@Input()` e emitindo eventos para as ações de editar e excluir via `@Output()`.
- Um componente `CurationFormModalComponent` deve ser criado no `src/app/shared/components/`.
    - Ele deve ser um componente "burro" que recebe um `FormGroup` e um título via `@Input()` e emite um evento de `save` com os dados do formulário via `@Output()`.

#### **AC4: Implementação de um Módulo Piloto para Validação**

- Para validar que as abstrações funcionam corretamente, a **primeira funcionalidade de curadoria, "Gerenciamento de Tecnologias",** deve ser completamente implementada usando os padrões criados nos ACs anteriores.
- Isso inclui:
    - Criar o `TechnologiesService` que herda de `BaseCurationService`.
    - Criar o `TechnologiesComponent` que herda de `BaseCurationComponent`.
    - Utilizar os componentes `CurationTableComponent` e `CurationFormModalComponent` em seu template.
- Ao final, o CRUD completo para a entidade "Tecnologias" deve estar 100% funcional, servindo como exemplo para a implementação de todas as outras páginas de curadoria.