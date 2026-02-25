---
theme: default
transition: fade
colorSchema: dark
lineNumbers: true
layout: image
image: /cover.svg
description: Programação Web 2
author: José Roberto Bezerra
title: Frontend Design
exportFilename: pw2_aula1_paradigmas
---

# {{ $slidev.configs.title }}
{{ $slidev.configs.description }}

---

# Objetivos de Aprendizagem
- Conhecer estratégias de desenvolvimento *Frontend*

---

# Agenda
- *Design Patterns*
- Abordagens de desenvolvimento
- 

---
layout: section
---

# *Design Patterns*

---

> Design **patterns** provide proven solutions to common problems in software development.

---

# *Design Patterns*
Propriedades
- Estruturas escaláveis e reutilizáveis
- Melhoria da mantenabilidade do código
- Robustez, eficiência, etc

---

# *Design Patterns*
Exemplos
- MVC (*Model-View-Controller*)
- Flux Architecture
- Dependency Injection
- Component-Based Architecture

---

# MVC

> The MVC pattern separates an application into three interconnected components: the Model, the View, and the Controller. The Model represents the data and business logic, the View handles the presentation and user interface, and the Controller acts as the intermediary between the Model and View

---

# Flux Architecture

> Flux is an application architecture pattern popularized by Facebook. It emphasizes unidirectional data flow and enforces strict separation of concerns between components: Actions, Stores, and Views.

---

# Dependency Injection

> Dependency Injection (DI) is a design pattern that aims to manage component dependencies by injecting them from external sources rather than creating them within the component itself.

---

# Component Based

> Component-Based Architecture emphasizes building applications by composing reusable UI components. It promotes encapsulation, modularity, and reusability.

---

# Component Based
Vantagens
- Reusability: Components can be easily reused across different parts of the application
- Encapsulation: Each component is responsible for its own state and behavior, enhancing code modularity and maintainability
- Development efficiency: Teams can work on individual components simultaneously, promoting parallel development

---

# Component Based
Desvantagens
- Complexity with large projects: As the number of components grows, managing inter-component communication and dependencies can become challenging
- Performance concerns: Improper component design or excessive rendering can impact performance
- Learning curve: Developers need to learn how to design and compose components effectively

---

# *Component-Based Architecture*

> Every modern frontend library recommends that developers build apps using component-based architecture. Browse any React, Angular, Vue, and Svelte apps to check the component-based architecture pattern

---
layout: section
---

# Arquiteturas de desenvolvimento

---

# Arquiteturas de desenvolvimento

- Static Site Generator (SSG)
- Single Page Application (SPA)
- Server-Side Rendering (SSR)

---

# Single Page Application (SPA)
- Content is loaded via Javascript files for the entire application and housed within a single HTML page
- The Javascript files house all the data relating to the application logic, UI, and communication with the server
- A medida que o usuário realiza requisições a página vai sendo modificada sem necessidade de novas transferências de dados

---

# Single Page Application (SPA)
Vantagens

- Experiência do usuário mais fluida e responsiva
- Menor tempo de resposta após o carregamento inicial
- Gerenciamento de estado mais complexo em grandes aplicações

---

# Single Page Application (SPA)
Desvantagens

- Tempo de carregamento cresce com a complexidade da aplicação
- Dificulta *Search Engine Optimization* (SEO)

---

# Single Page Application (SPA)
Quando usar?

- Dashboards e aplicações mais interativas
- Evitar utilizar para aplicações que dependem de SEO, ou seja que possuem conteúdo intensivo

---

# Server-Side Rendering (SSR)

- Os clientes recebem uma página já renderizada no servidor
- A renderização ocorre no servidor antes de chgar no navegador, após consultas a bancos de dados, APIs, etc 
- Alguns elementos podem ser armazenados em cache

---

# Server-Side Rendering (SSR)
Vantagens

- Changes to content are displayed instantaneously unlike SSGs where teams must rebuild the site to see the changes to the content
- SSR enables teams to create dynamic, personalized content experiences without labor-intensive workarounds
- Facilita a classificação por motores de busca (SEO)

---

# Server-Side Rendering (SSR)
Desvantagens

- SSRs typically require more API calls to the server
- SSRs by default are often slower than SPAs and SSGs

---

# Server-Side Rendering (SSR)
Quando aplicar?

> They are ideal for personalized experiences where live changes to the data can be viewed.Server-side rendered sites (or server-side rendered applications (SRAs)) are excellent choices for content that is time-sensitive and applications that rely on large amounts of user interaction

---

# Static Site Generator (SSG)
- generate content at the build time of new pages or when changes are made to the content
- there is no need to load pages based on user requests

--- 

# Static Site Generator (SSG)
Vantagens
- Criação do conteúdo desacoplada da arquitetura
- Carregamento rápido
- Melhor para otimização de busca (SEO)

---

# Static Site Generator (SSG)
Desvantagens
- Dificuldade para aplicar conteúdos dinâmicos
- Mudança de conteúdo requer recriar o site (*rebuild*)

---

# Static Site Generator (SSG)
Quando usar?
- Sites estáticos
- CDN (*Content Delivery Network*)

---
layout: section
---

# Frameworks

---

# React
*Single Page Application*

> React é usado para criar uma aplicação que roda inteiramente no navegador do cliente após o carregamento inicial.

---

# React
*Single Page Application*

- Funcionamento: O servidor envia um arquivo HTML praticamente vazio com uma div root. Todo o conteúdo da interface é gerado e gerenciado no lado do cliente (client-side) usando JS
- Ferramentas comuns: As ferramentas recomendadas são o Vite (que substituiu o antigo Create React App) ou o modo "SPA" de frameworks mais completos, como o React Router (antigo Remix)
- Quando usar: Ideal para aplicações internas, dashboards administrativos ou qualquer projeto onde o SEO (otimização para mecanismos de busca) não é um fator crítico e a experiência rica e interativa no cliente é prioridade .

---

# React
*Server-Side Rendering*

> Nesta arquitetura, o React é executado no servidor para gerar o HTML completo da página, que é então enviado ao cliente.

---

# React
*Server-Side Rendering*

- Funcionamento: O servidor (geralmente Node.js) usa funções como `renderToString` para transformar os componentes React em HTML
- Cada HTML é renderizado imediatamente no navegador, proporcionando uma sensação de carregamento mais rápido. Em seguida, o código JS do React é carregado e assume o controle no processo chamado de hidratação (`hydration`), tornando a página interativa 

---

# React
*Server-Side Rendering*

- Ferramentas comuns: A implementação manual de SSR com React e Node.js é possível, mas complexa. Por isso, a própria documentação do React recomenda o uso de frameworks que já incorporam essa funcionalidade, como o Next.js (na sua arquitetura Pages Router) ou o React Router (com SSR ativado)
- Quando usar: Essencial para sites de conteúdo, blogs, e-commerces e qualquer aplicação que dependa de um bom SEO e de um carregamento rápido da primeira página para uma melhor experiência do usuário

---

# Abordagem Híbrida
*Frameworks Modernos*

> Frameworks como Next.js e React Router (antigo Remix) são frequentemente chamados de "híbridos" porque combinam o melhor dos dois mundos

---

# Abordagem Híbrida
*Frameworks Modernos*

- A primeira visita a uma página pode ser feita com SSR, servindo HTML completo para carregamento rápido e SEO
- A navegação entre páginas subsequente acontece no cliente, como em uma SPA, sem recarregar a página inteira, o que torna a navegação muito fluida

---

# Referências

- [5 Design Patterns on the Frontend](https://medium.com/design-bootcamp/exploring-5-patterns-on-the-frontend-pros-and-cons-a1591d4ea9f2)
- [Guide to modern frontend architecture patterns](https://blog.logrocket.com/guide-modern-frontend-architecture-patterns/)
- [About React and Next.js](https://nextjs.org/learn/react-foundations/what-is-react-and-nextjs)

---
src: /snippets/end.md
---