# ADR 0001: Uso de Angular Signals para Gerenciamento de Estado

**Status:** Aceito

**Data:** 2025-06-14

## Contexto

Para o desenvolvimento da aplicação em Angular 20, precisamos de uma estratégia de gerenciamento de estado que seja reativa, performática e de fácil manutenção. As principais alternativas consideradas foram:
1.  **RxJS (BehaviorSubject):** Padrão tradicional no Angular, poderoso, mas pode levar a um excesso de boilerplate e complexidade no gerenciamento de subscriptions.
2.  **Bibliotecas de Estado (NgRx, Akita):** Soluções robustas e com boas ferramentas, mas que adicionam uma camada significativa de complexidade e dependências ao projeto, sendo excessivas para o nosso escopo atual.
3.  **Angular Signals:** Nova primitiva de reatividade introduzida no Angular, projetada para ser mais simples e otimizada para detecção de mudanças granulares.

## Decisão

Adotaremos **Angular Signals** como a principal ferramenta para gerenciamento de estado reativo dentro dos componentes e serviços da aplicação. Isso inclui o uso de `signal()`, `computed()`, e `effect()` para modelar o estado da UI, dados carregados e reações a mudanças de estado.

O RxJS continuará a ser utilizado em seu ponto forte: o gerenciamento de eventos assíncronos complexos, especialmente em chamadas HTTP nos serviços. A integração entre os dois mundos será feita através do `toSignal` do `@angular/core/rxjs-interop`.

## Consequências

**Positivas:**
* **Código mais simples e legível:** Redução drástica de boilerplate em comparação com soluções baseadas em RxJS puro para estado.
* **Performance Otimizada:** A reatividade granular dos Signals permite que o Angular atualize apenas os componentes que realmente precisam mudar.
* **Alinhamento com o futuro do Angular:** Adoção de uma prática moderna e recomendada pelo time do Angular.
* **Curva de aprendizado mais suave** para novos desenvolvedores em comparação com bibliotecas de estado complexas.

**Negativas:**
* A equipe precisa estar confortável com o paradigma dos Signals e entender quando ainda é apropriado usar RxJS.
* Requer disciplina para gerenciar a interação entre Observables e Signals de forma eficaz.