---
theme: default
transition: fade
colorSchema: dark
lineNumbers: true
layout: image
image: /cover.svg
description: Programação Web 2
author: José Roberto Bezerra
title: React
exportFilename: pw2_aula2_hello_react
---

# {{ $slidev.configs.title }}
{{ $slidev.configs.description }}

---

# Objetivos de Aprendizagem
- Conhecer características do React
- Criar a primeira aplicação usando React

---

# Agenda
- Conceito e características
- JSX
- Configurando ambiente

---
layout: section
---

# Conceito e características

---
layout: quote
---

> React é uma biblioteca JS para a criação de interfaces de usuário web. Permite a criação de **componentes** reutilizáveis. React é usado essencialmente para criar *Single Page Applications* (SPA)

---
layout: quote
---

> React foi desenvolvido pelo Facebook (hoje Meta) pelo engenheiro Jordan Walke. Em 2011 como uma ferra


---

# React
- Interfaces construídas a partir de pequenas partes reutilizáveis (componentes)
- Permite ainda a criação de componentes personalizados
- A combinação de componentes nativos e personalizados compõe a interface

---
layout: image-right
backgroundSize: contain
image: https://nextjs.org/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Flearn%2Fdark%2Flearn-react-components.png&w=1920&q=75
---

# React
Componentes
- Um componente é basicamente um conjunto de funções JS
- A sintaxe utilizada é o JSX, uma extensão do JS que combina a sintaxe JavaScript com marcações HTML 

---
layout: section
---

# JSX

---

# JSX
- A web foi fundamentada em HTML (conteúdo), CSS (*design*) e lógica (JS), normalmente em arquivos separados
- Com uma Internet mais interativa, a lógica passou a determinar cada vez mais o conteúdo
- A ideia do React+JSX é manter lógica de renderização e marcação juntas
- Como cada componente é uma função que retorna a marcação a ser renderizada no navegador

---
layout: image
image: https://pt-br.react.dev/_next/image?url=%2Fimages%2Fdocs%2Fdiagrams%2Fwriting_jsx_form.dark.png&w=384&q=75
backgroundSize: contain
---

# Componente React `Form.js`

---
layout: two-cols-header
---

# JSX
Primeiras regras

1. Retornar um único elemento raiz

:: left ::

```js
<h1>Tarefas de Hedy Lamarr</h1>
<img 
  src="https://i.imgur.com/yXOvdOSs.jpg" 
  alt="Hedy Lamarr" 
  class="photo"
>
<ul>
    <li>Inventar novos semáforos
    <li>Ensaio de uma cena de filme
    <li>Melhorar a tecnologia de espectro
</ul>
```

:: right ::

```js
export default function TodoList() {
  return (
    // ???
  )
}
```

---

# JSX
Primeiras regras

2. Todas as *tags* explicitamente fechadas

```js
<>
  <img 
    src="https://i.imgur.com/yXOvdOSs.jpg" 
    alt="Hedy Lamarr" 
    class="photo"
   />
  <ul>
    <li>Inventar novos semáforos</li>
    <li>Ensaio de uma cena de filme</li>
    <li>Melhorar a tecnologia de espectro</li>
  </ul>
</>
```

---

# JSX
Primeiras regras

3. `camelCase`

> JSX se transforma em JavaScript e atributos escritos em JSX se tornam chaves de objetos JS. Porém, o JS tem limitações nos nomes das variáveis, por exemplo seus nomes não podem conter hífens ou ser palavras reservadas como `class`.

---

# JSX
Primeiras regras

3. `camelCase`

> Por isso que, no React, muitos atributos HTML e SVG são escritos em `camelCase`. Por exemplo, em vez de `stroke-width`, utiliza-se `strokeWidth`. Como `class` é uma palavra reservada, no React escreve-se `className`

```js
<img 
  src="https://i.imgur.com/yXOvdOSs.jpg" 
  alt="Hedy Lamarr" 
  className="photo"
/>
```

---

# JSX
Conversor

[transform HTML to JSX](https://transform.tools/html-to-jsx)

---
layout: section
---

# Configurando o Ambiente

---

# Requisitos
- JavaScript (Nodejs)
- Gerenciador de pacotes (NPM, Yarn, PNPM, etc)
- Ferramenta de montagem (*build tool*)
    - `create-react-app`
    - webpack
    - Rollup
    - Parcel
    - Vite

---

# Por que Vite?

> A quantidade de módulos JS para desenvolvimento de projetos cresce com a complexidade dos mesmos. Grandes projetos podem conter milhares de módulos podendo levar minutos para um servidor ficar disponível. Vite pretende solucionar essa questão.

---

# Como Vite Funciona?
- Os módulos são divididos em duas categorias
    - Dependencies
    - Source code
- ***Dependencies*** passam pelo processo chamado *pre-bundle* utilizando a linguagem Go (10-100x mais rápido do que JS)
- O código fonte apenas é transformado sob demanda no navegador num processo chamado *native ESM* (*EcmaScript Module*)

---
layout: image
image: https://cdn.shopify.com/s/files/1/0779/4361/files/bundle_based_dev_server.png?v=1648583556
backgroundSize: contain
---

# Bundling

---
layout: image
image: https://cdn.shopify.com/s/files/1/0779/4361/files/native_ESM_based_dev_server.png?v=1648583809
backgroundSize: contain
---

# Native ESM

---

# Criando o Primeiro Projeto
Checar nodejs e npm

```bash
node --version
npm --version
```

---

# Criando o Primeiro Projeto
Criar a estrutura (*scaffolding*)

```bash
npm create vite@latest
```

> Na sequência serão feitas algumas perguntas.

---

# Criando o Primeiro Projeto
`npm create vite@latest`

- `Project name` use `.` para usar o diretório corrente ou um nome para criar o diretório do projeto
- `Framework` para esse exemplo utilizar React
- `Variante` para esse exemplo utilizar JavaScript

---

# Criando o Primeiro Projeto
Instalar as dependências

```bash
npm install
```

---

# Criando o Primeiro Projeto
Rodar a aplicação

```bash
npm run dev
```

---
layout: image-right
image: https://www.w3schools.com/react/screenshot_react1.png
backgroundSize: contain
---

[http://localhost:5173](http://localhost:5173)

---

# Criando o Primeiro Projeto
Estrutura de diretórios

- `/public` served directly to browsers without any processing (*as-is*)
- `/src`
    - `/assets` Assets here go through the build process, get optimized, and can be imported into your components
- `index.html` The main HTML file for your application. Vite serves this file as the entry point and injects the necessary scripts and styles.
- `vite.config.json` arquivo de configuração

---
layout: fact
---

# Perguntas

---
layout: fact
---

# Exercícios

---

# 1
Crie uma aplicação React utilizando o Vite no seu ambiente local.


---

# 2
Crie a mesma aplicação agora no serviço EC2 da AWS.

---

# 3
Busque um outro provedor de serviços de computação em nuvem para realizar operação similar ao exercício anterior.


---

# Referências

- [React](https://react.dev/)
- [Meta Open Source](https://opensource.fb.com/projects/react/)
- [First React Project with Vite](https://scrimba.com/intro-to-vite-c03p6pbbdq/~0yhj?via=vite)
- [public x assets](https://www.thatsoftwaredude.com/content/14144/public-vs-src-assets-when-to-use-each-approach-in-vite)

---
src: /snippets/end.md
---