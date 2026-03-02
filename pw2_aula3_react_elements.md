---
theme: default
transition: fade
colorSchema: dark
lineNumbers: true
layout: image
image: /cover.svg
description: Programação Web 2
author: José Roberto Bezerra
title: Elementos de Apps React
exportFilename: pw2_aula3_react_elements
---

# {{ $slidev.configs.title }}
{{ $slidev.configs.description }}

---

# Objetivo de Aprendizagem
- Conhecer os elementos de uma aplicação React

---

# Agenda
- Aplicação de demonstração Vite + React 

---
layout: section
---

# Vite + React Demo

---

```js
import { useState } from 'react'
import reactLogo from './assets/react.svg'
import viteLogo from '/vite.svg'
import './App.css'

function App() {
  const [count, setCount] = useState(0)

  return (
    <>
      <div>
        <a href="https://vitejs.dev" target="_blank">
          <img src={viteLogo} className="logo" alt="Vite logo" />
        </a>
        <a href="https://react.dev" target="_blank">
          <img src={reactLogo} className="logo react" alt="React logo" />
        </a>
      </div>
      <h1>Vite + React</h1>
      <div className="card">
        <button onClick={() => setCount((count) => count + 1)}>
          count is {count}
        </button>
        <p>
          Edit <code>src/App.jsx</code> and save to test HMR
        </p>
      </div>
      <p className="read-the-docs">
        Click on the Vite and React logos to learn more
      </p>
    </>
  )
}

export default App
```


---

# Importando Recursos 
`useState`

```js
import { useState } from 'react'
import reactLogo from './assets/react.svg'
import viteLogo from '/vite.svg'
import './App.css'

function App() {
  const [count, setCount] = useState(0)
```

---
layout: quote
---

>  O estado (*state*) permite gerenciar dados alterados em uma aplicação. Quando o *state* é modificado por alguma ação do usuário (clique, digitação, etc) a página é novamente renderizada

---

# State

- Para a aplicação demo o estado consiste na variável `count` que representa a contagem de cliques no botão
- `setCount` é a função que modifica `count`
- `useState()` é um exemplo de *hook*. O estado é manipulado através de *hooks*
- `useState(0)` inicializa o estato inicial (variável `count`) com valor zero

---

# Importando Recursos 

- `/assets` recursos nesse diretório passam por otimização (*build*)

```js
import { useState } from 'react'
import reactLogo from './assets/react.svg'
import viteLogo from '/vite.svg'
import './App.css'
```

---

# React Functional Components

- Na aplicação demo temos um único componente `App()`
- Um componente React é apenas uma função JS que retorna JSX
- JSX é uma mistura de código JS e tags HTML

---

# Tag Única
- Observar as linhas 10 e 31

```js
return (
    <>
      <div>
        <a href="https://vitejs.dev" target="_blank">
          <img src={viteLogo} className="logo" alt="Vite logo" />
        </a>
        <a href="https://react.dev" target="_blank">
          <img src={reactLogo} className="logo react" alt="React logo" />
        </a>
      </div>
      <h1>Vite + React</h1>
      <div className="card">
        <button onClick={() => setCount((count) => count + 1)}>
          count is {count}
        </button>
        <p>
          Edit <code>src/App.jsx</code> and save to test HMR
        </p>
      </div>
      <p className="read-the-docs">
        Click on the Vite and React logos to learn more
      </p>
    </>
  )
```

---

# Modificando *State*
- Observar a linha 13
- A interação do usuário (clique) altera *state*
- A cada clique o *event listener* associado ao botão é chamado(`setCount`)
- `setCount` modifica o estado o que forçando que a página seja renderizada novamente com *state* atualizado

```js {}
<button onClick={() => setCount((count) => count + 1)}>
    count is {count}
</button>
```

---

# Disponibilizando o Componente
`App`
- Observar a última linha
- Disponibiliza o componente de nome `App` para ser importado por `main.jsx` (responsável pela renderização)

```js
export default App
```

---

# Modificando o Componente
- Atualizar App.jsx como mostrado
- Observar que a página é rendereizada logo após a modificação do arquivo

```js
function App() {
  return (
    <div className="App">
      <h1>Hello World!</h1>
    </div>
  );
}

export default App
```

---
layout: section
---

# Renderização

---

# Renderização
`createRoot()`
- A grande funcionalidade do React é renderizar HTML
- A renderização acontece através do *container* `createRoot()`
- Tipicamente, é estruturado como uma <div id="root"></div> no `index.html`

---

# `index.html`
Observar linhas 10-11

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" type="image/svg+xml" href="/vite.svg" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Vite + React</title>
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.jsx"></script>
  </body>
</html>
```

---

# `main.jsx`

```js
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import './index.css'
import App from './App.jsx'

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <App />
  </StrictMode>,
)

```

---

# `main.jsx`
`StrictMode`
- Ferramenta puramente de desenvolvimento
- Destaca potenciais problemas no código
- Fornece *warnings*, etc

---

# `main.jsx`
`createRoot()`
- Encontra `<div id="root">` no `index.html`
- A partir desse ponto a aplicação React é montada
- A renderização é efetivamente realizada por `.render(<App />)`

---

# `render()`
- Define o que deve ser renderizado no *container* HTML
- Outro exemplo de `main.jsx`

```js
import { createRoot } from 'react-dom/client'

createRoot(document.getElementById('root')).render(
  <p>Welcome!</p>
) 
```

---

# `render()`
Exemplo

```js
import { createRoot } from 'react-dom/client'

const myelement = (
  <table>
    <tr>
      <th>Name</th>
    </tr>
    <tr>
      <td>John</td>
    </tr>
    <tr>
      <td>Elsa</td>
    </tr>
  </table>
);

createRoot(document.getElementById('root')).render(
  myelement
)
```

---
layout: two-cols-header
---

# Alterando o Nó Raiz
*Root Node*

:: left ::

### `index.html`

```js
<!doctype html>
<html lang="en">
  <body>
    <header id="sandy"></header>
    <script type="module" src="/src/main.jsx"></script>
  </body>
</html>
```

:: right ::

### `main.jsx`

```js
import { createRoot } from 'react-dom/client'

createRoot(document.getElementById('sandy')).render(
  <p>Welcome!</p>
) 
```

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
Crie uma aplicação React utilizando o Vite no seu ambiente local. Deixe a aplicação rodando. Modifique a aplicação como mostrado na aula. O que acontece? Foi preciso reiniciar o navegador?

---

# 2
Repita o procedimento da questão anterior utilizando o provedor de serviços de nuvem Digital Ocean.

---

# Referências

- [React Tutorial W3Schools](https://www.w3schools.com/react/default.asp)
- [React](https://react.dev/)

---
src: /snippets/end.md
---