# ADR 0003: Adoção de Angular com SSR para o Frontend

**Status:** Decidido

**Data:** 2025-06-10

## Contexto

O projeto Talent Flow exige uma interface web moderna e reativa para a experiência do usuário (candidatos e RH). Ao mesmo tempo, possui um requisito de negócio crucial: as páginas de divulgação de vagas devem ser públicas e otimizadas para motores de busca (SEO), a fim de garantir a máxima visibilidade e atrair candidatos organicamente. Uma aplicação Single-Page Application (SPA) padrão teria dificuldades em atender ao requisito de SEO de forma eficaz.

## Decisão

Decidimos utilizar **Angular 20 com Server-Side Rendering (SSR) via Angular Universal**. A aplicação será construída de forma "Zoneless", utilizando **Angular Signals** como o principal mecanismo para gerenciamento de estado e detecção de mudanças. Esta abordagem combina a reatividade e a experiência de uma SPA com a performance de carregamento inicial e a indexabilidade de uma aplicação renderizada no servidor.

## Consequências

**Positivas:**
* **SEO Otimizado:** O SSR garante que os motores de busca recebam páginas HTML completas, permitindo a indexação eficiente das vagas públicas.
* **Performance Percebida:** Melhora o First Contentful Paint (FCP), pois o usuário recebe uma página renderizada imediatamente.
* **Código Moderno e Reativo:** O uso de Signals e da arquitetura Zoneless resulta em uma aplicação mais performática e com um código mais simples e legível.
* **Ecossistema Robusto:** O Angular oferece um framework completo com ferramentas integradas para roteamento, formulários e requisições HTTP.

**Negativas:**
* **Complexidade de Deploy:** A aplicação com SSR requer um ambiente de servidor Node.js para ser executada (via Cloud Run, conforme decidido), o que é mais complexo do que o deploy de uma SPA estática.
* **Gerenciamento de Estado:** É preciso ter cuidado para gerenciar o estado que é transferido do servidor para o cliente (State Transfer) para evitar duplicação de chamadas de API durante o processo de *hydration*.