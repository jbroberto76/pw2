---
theme: default
transition: fade
colorSchema: dark
lineNumbers: true
layout: image
image: /cover.svg
description: Programação Web 2
author: José Roberto Bezerra
title: Eventos React
exportFilename: pw2_aula7_eventos
---

# {{ $slidev.configs.title }}
{{ $slidev.configs.description }}

---

# Objetivos de Aprendizagem
- Compreender o uso de eventos na perspectiva do React
- Utilizar eventos em interfaces web

---

# Agenda

- Eventos
- Renderização Condicional
- Listas
- Formulários
- *Hooks*

---
layout: section
---

# Eventos React

---
layout: quote
---

# Eventos React

> Assim como os eventos DOM do HTML, o React pode executar ações com base em eventos do usuário, tais como cliques, alteração de campos de formulário, movimento do mouse, etc.

---

# Adicionando Eventos

- Usar sintaxe `camelCase`
    - `onClisk` ao invés de ~~`onclick`~~
- *Event handlers* devem estar entre `{ }`
    - `onClick={shoot}` ao invés de ~~`onclick="shoot()"`~~

```js {*}{class: '!children:text-xl'}
<button onClick={shoot}>Take the Shot!</button>
```

---

```js {*}{class: '!children:text-xl'}
function Football() {
  const shoot = () => {
    alert("Great Shot!");
  }

  return (
    <button onClick={shoot}>Take the shot!</button>
  );
}

createRoot(document.getElementById('root')).render(
  <Football />
);
```

---

# Passando Argumentos
Argumentos são passados utilizando *arrow functions*

```js {*}{class: '!children:text-xl'}
function Football() {
  const shoot = (a) => {
    alert(a);
  }

  return (
    <button onClick={() => shoot("Goal!")}>Take the shot!</button>
  );
}

createRoot(document.getElementById('root')).render(
  <Football />
);
```

---
layout: quote
---

# React Event Object

> Os manipuladores de eventos têm acesso ao evento React que disparou a função. Em nosso exemplo, o evento é o "click".

---

```js {*}{class: '!children:text-xl'}
function Football() {
  const shoot = (a, b) => {
    alert(b.type);
    /*
    'b' represents the React event that triggered the function,
    in this case the 'click' event
    */
  }

  return (
    <button onClick={(event) => shoot("Goal!", event)}>Take the shot!</button>
  );
}

createRoot(document.getElementById('root')).render(
  <Football />
);
```

[Veja o exemplo!](https://www.w3schools.com/react/showreact.asp?filename=demo_react_events3)

---
layout: section
---

# Renderização Condicional

---

# `if`
Exemplo 1

```js {*}{class: '!children:text-xl'}
function MissedGoal() {
  return <h1>MISSED!</h1>;
}

function MadeGoal() {
  return <h1>Goal!</h1>;
}
```

---

# Exemplo 1

> O terceiro componente decide qual dos componentes anteriores utilizar

```js {*}{class: '!children:text-xl'}
function Goal(props) {
  const isGoal = props.isGoal;
  if (isGoal) {
    return <MadeGoal/>;
  }
  return <MissedGoal/>;
}

createRoot(document.getElementById('root')).render(
  <Goal isGoal={false} />
);
```

---

# Operador `&&`

> Outra forma de implementar renderização lógica é usando o operador `&&`

---

# Operador `&&`
Exemplo 2

```js {*}{class: '!children:text-xl'}
function Car(props) {
  return (
    <>
      {props.brand && <h1>My car is a {props.brand}!</h1>}
    </>
  );
}

createRoot(document.getElementById('root')).render(
  <Car brand="Ford" />
);
```

[Veja o exemplo!](https://www.w3schools.com/react/showreact.asp?filename=demo_react_conditionals_logical2)

---

# Operador Ternário
Exemplo 3

```js {*}{class: '!children:text-xl'}
function Goal(props) {
  const isGoal = props.isGoal;
  return (
    <>
      { isGoal ? <MadeGoal/> : <MissedGoal/> }
    </>
  );
}

createRoot(document.getElementById('root')).render(
  <Goal isGoal={false} />
);
```

---
layout: section
---

# Listas

---
layout: quote
---

# Listas

> Em React as listas são geradas através de laços e `map()`

---

```js {*}{class: '!children:text-xl'}
function MyCars() {
  const cars = ['Ford', 'BMW', 'Audi'];
  return (
    <>
      <h1>My Cars:</h1>
      <ul>
        {cars.map((car) => <li>I am a { car }</li>)}
      </ul>
    </>
  );
}

createRoot(document.getElementById('root')).render(
  <MyCars />
);
```

---

# Listas React com Chaves

- As chaves permitem que o React rastreie os elementos da lista
- Se um item for atualizado ou removido, apenas esse item será renderizado novamente, em vez da lista inteira
- Chaves devem ser únicas entre os elementos, mas não precisam ser únicas em toda a aplicação

---

# Listas
Exemplo 4

```js {*}{class: '!children:text-xl'}
function MyCars() {
  const cars = [
    {id: 1001, brand: 'Ford'},
    {id: 1002, brand: 'BMW'},
    {id: 1003, brand: 'Audi'}
  ];
  return (
    <>
      <h1>My Cars:</h1>
      <ul>
        {cars.map((car) => <li key={car.id}>I am a { car.brand }</li>)}
      </ul>
    </>
  );
}

createRoot(document.getElementById('root')).render(
  <MyCars />
);
```


---

# Listas
Exemplo 4 modificado

```js {*}{class: '!children:text-xl'}
function MyCars() {
  const cars = ['Ford', 'BMW', 'Audi'];
  return (
    <>
      <h1>My Cars:</h1>
      <ul>
        {cars.map((car, index) => <li key={index}>I am a { car }</li>)}
      </ul>
    </>
  );
}

createRoot(document.getElementById('root')).render(
  <MyCars />
);
```

---
layout: section
---

# Formulários

---

# HTML versus React

- Em React, elementos de formulário como `<input>`, `<textarea>` e `<select>` funcionam diferentemente do HTML tradicional
    - **HTML**, os elementos de formulário mantêm seu próprio valor com base na entrada do usuário
    - Por exemplo, um campo `<input type="text">` mantém o controle do seu próprio valor no DOM do HTML.
- **React**, o valor do elemento de formulário é mantido na propriedade `state` do componente e atualizado apenas com a função `setState()`

> O React oferece uma maneira de gerenciar os dados do formulário por meio do estado do componente, resultando no que é conhecido como "componentes controlados".

---

# Componentes Controlados
*Controlled components*

- Dados de formulários são gerenciados pelo componente React
- O valor de `<input>`, por exemplo faz parte do *state*
- Dados gerenciados pelo componente são armazenados no próprio componente
- `useState` deve ser utilizado para cada entrada

---

# Exemplo 5

```js {*}{class: '!children:text-sm'}
import { useState } from 'react';
import { createRoot } from 'react-dom/client';

function MyForm() {
  const [name, setName] = useState("");

  function handleChange(e) {
    setName(e.target.value);
  }

  return (
    <form>
      <label>Enter your name:
        <input type="text" value={name} onChange={handleChange} />
      </label>
      <p>Current value: {name}</p>
    </form>
  )
}

createRoot(document.getElementById('root')).render(
  <MyForm />
);
```

---

```js {*}{class: '!children:text-sm', maxHeight:'480px'}
import { useState } from 'react';
import { createRoot } from 'react-dom/client';

function MyForm() {
  const [name, setName] = useState("");

  function handleChange(e) {
    setName(e.target.value);
  }

  function handleSubmit(e) {
    e.preventDefault();
    alert(name);
  }

  return (
    <form onSubmit={handleSubmit}>
      <label>Enter your name:
        <input
          type="text" 
          value={name}
          onChange={handleChange}
        />
      </label>
      <input type="submit" />
    </form>
  )
}

createRoot(document.getElementById('root')).render(
  <MyForm />
);
```

---
layout: section
---

# *Hooks*

---
layout: quote
---

# *Hooks*

> Hooks permitem que as funções acessem o estado e outros recursos do React sem usar classes

---

# *Hooks*

- Precisam ser importadas
    - `import { useState } from 'react';`
- `useState` é um *hook* que monitora o estado da aplicação (dados ou propriedades)

---

# *Hooks*
Regras de uso

- Apenas podem ser chamadas dentro de um componente
- Não podem ser condicionais
- Apenas podem ser chamadas no primeiro nível de um componente
- Não funcionam em componentes de classe

---

# `useState`
Exemplo

```js {*}{class: '!children:text-xl'}
import { useState } from "react";

function FavoriteColor() {
  const [color, setColor] = useState("red");
}
```

---

# `useState`
Lendo o estado

```js {*}{class: '!children:text-xl'}
import { useState } from 'react';
import { createRoot } from 'react-dom/client';

function FavoriteColor() {
  const [color, setColor] = useState("red");

  return <h1>My favorite color is {color}!</h1>
}

createRoot(document.getElementById('root')).render(
  <FavoriteColor />
);
```

---

# `useState`
Atualizando o estado

```js {*}{class: '!children:text-xl'}
<button
  type="button"
  onClick={() => setColor("blue")}
>Blue</button>
```

---

# `useState`
Objeto *state*

```js {*}{class: '!children:text-xl', maxHeight:'480px'}
import { useState } from 'react';
import { createRoot } from 'react-dom/client';

function MyCar() {
  const [car, setCar] = useState({
    brand: "Ford",
    model: "Mustang",
    year: "1964",
    color: "red"
  });

  return (
    <>
      <h1>My {car.brand}</h1>
      <p>
        It is a {car.color} {car.model} from {car.year}.
      </p>
    </>
  )
}

createRoot(document.getElementById('root')).render(
  <MyCar />
);
```

---

# `useState`
Atualizando objetos *state*

```js {*}{class: '!children:text-xl'}
const updateColor = () => {
  setCar(previousState => {
    return { ...previousState, color: "blue" }
  });
}
```

---

# Outros *Hooks*
- `setEffect`
- `useContext`
- `useRef`
- `useReducer`
- `useCallback`
- `useMemo`
- *Hooks* Personalisadas

> Próxima Aula


---
layout: fact
---

# Perguntas?

---
layout: fact
---

# Exercício

---

# 1
Crie um componente React que permita ao usuário:

- Adicionar novas tarefas via um formulário com um campo de input e botão de *submit*
- Exibir a lista de tarefas usando `map()` para renderizar cada item
- Marcar tarefas como concluídas ou não concluídas com um evento de clique (ex.: *checkbox* ou botão)
- Remover tarefas com um botão de deletar
- Usar renderização condicional para mostrar apenas tarefas pendentes ou todas, com base em um filtro (ex.: botões "Todas", "Pendentes", "Concluídas").

---

# 1
Estrutura básica

```js
import React, { useState } from 'react';

function TodoList() {
  const [tasks, setTasks] = useState([]);
  const [input, setInput] = useState('');
  const [filter, setFilter] = useState('all');

  // Funções para adicionar, toggle e remover tarefas
  // Renderização condicional para o filtro
  // Lista mapeada com eventos

  return (
    <div>
      <form onSubmit={handleAddTask}>
        <input value={input} onChange={(e) => setInput(e.target.value)} />
        <button type="submit">Adicionar</button>
      </form>
      {/* Filtros e lista */}
    </div>
  );
}
```

---

# 1 
Dicas

- Aplique `useState` para gerenciar o estado da lista de tarefas, do `input` do formulário e do filtro
- Implemente eventos como `onSubmit` no formulário, `onClick` nos botões e `onChange` no input.
- Aplique renderização condicional com operador ternário ou `&&` para o filtro e para estilizar tarefas concluídas (ex.: texto riscado).
- Estruture o componente em JSX, com listas renderizadas dinamicamente

---

# 1

> Postar os resultados na Atividade ToDo List do Google Classroom

---

# Referências

- [React Documentation](https://react.dev)
- [W3Schools React Components](https://www.w3schools.com/react/react_components.asp)
- [React DevTools](https://react-devtools-tutorial.vercel.app/)

---
src: /snippets/end.md
---