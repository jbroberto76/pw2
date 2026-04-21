---
theme: default
transition: fade
colorSchema: dark
lineNumbers: true
layout: image
image: /cover.svg
description: Programação Web 2
author: José Roberto Bezerra
title: React Hooks
exportFilename: pw2_aula8_hooks
---

# {{ $slidev.configs.title }}
{{ $slidev.configs.description }}

---

# Objetivos de Aprendizagem
- Compreender o funcionamento de Hooks
- Aplicar Hooks nas interfaces web

---

# Agenda

- Hooks
- `useState`
- `useEffect`
- `useContext`
- `useRef`
- `useReducer`
- `useCallback`
- `useMemo`

---
layout: section
---

# React Hooks

---
layout: quote
---

# React Hooks

> Hooks permitem que funções acessem o estado e outras funções do React sem utilizar classes

---

# React Hooks
Tipos

- State hooks
- Context hooks
- Ref hooks
- Effect hooks
- Performance hooks
- Custom

---

# State Hooks

> O estado permite que um componente "lembre" informações como a entrada do usuário. Por exemplo, um componente de formulário pode usar o estado para armazenar o valor de entrada, enquanto um componente de galeria de imagens pode usar o estado para armazenar o índice da imagem selecionada.

- `useState` declara uma variável de estado que você pode atualizar diretamente
- `useReducer` declara uma variável de estado com a lógica de atualização dentro de uma função `reducer`

---

# Context Hooks
`useContext`

> Permite que um componente receba informações de componentes pais distantes sem precisar passá-las como propriedades. Por exemplo, o componente de nível superior do seu aplicativo pode passar o tema da interface do usuário atual para todos os componentes abaixo dele, independentemente da profundidade na hierarquia.

```js
function Button() {
  const theme = useContext(ThemeContext);
  // ...
```

---

# Ref Hooks

> As refs permitem que um componente armazene informações que não são usadas para renderização, como um nó DOM ou um ID de tempo limite. Ao contrário do estado, atualizar uma `ref` não renderiza o componente novamente. As refs são uma "saída de emergência" do paradigma React. Elas são úteis quando você precisa trabalhar com sistemas que não são do React, como as APIs nativas do navegador.

- `useRef` declara uma referência. Você pode armazenar qualquer valor nela, mas geralmente é usada para armazenar um nó DOM.
- `useImperativeHandle` permite personalizar a referência exposta pelo seu componente. Isso raramente é usado.

---

# Effect Hooks

> Os efeitos permitem que um componente se conecte e sincronize com sistemas externos. Isso inclui lidar com rede, DOM do navegador, animações, widgets escritos usando uma biblioteca de interface do usuário diferente e outros códigos que não são do React.

- `useEffect` conecta um componente a um sistema externo

---

# Performance Hooks

> Uma maneira comum de otimizar o desempenho de renderização é evitar tarefas desnecessárias. Por exemplo, você pode instruir o React a reutilizar um cálculo em cache ou a ignorar uma nova renderização se os dados não tiverem sido alterados desde a renderização anterior.

- `useMemo` permite armazenar em cache o resultado de um cálculo custoso
- `useCallback` permite armazenar em cache a definição de uma função antes de passá-la para um componente otimizado
- `useTransition` permite marcar uma transição de estado como não bloqueante e permitir que outras atualizações a interrompam
- `useDeferredValue` permite adiar a atualização de uma parte não crítica da interface do usuário e permitir que outras partes sejam atualizadas primeiro

---
layout: section
---

# `useState`

---

# `useState`

- Chamada nas declarações iniciais de um componente para declarar uma variável de **estado**
- A convenção é nomear variáveis ​​de estado como `[something, setSomething]` usando desestruturação de *array*

```js
import { useState } from 'react';

function MyComponent() {
  const [age, setAge] = useState(28);
  const [name, setName] = useState('Taylor');
  const [todos, setTodos] = useState(() => createTodos());
  // ...
```

---

# `useState`

- `useState` retorna um array com dois valores: 
    - O estado atual. Durante a primeira renderização, ele corresponderá ao `initialState` passado
    - A função `set` que permite atualizar o estado para um valor diferente e acionar uma nova renderização
- `useState` não pode ser chamado em *loops* ou condicionais

---

# Funções `set`

- Funções `set` retornadas por `useState` permitem atualizar o estado para um valor diferente e acionar uma nova renderização
- Não retornam valor
- É possível passar o próximo estado diretamente ou uma função que o calcula a partir do estado anterior:

```js
const [name, setName] = useState('Edward');

function handleClick() {
  setName('Taylor');
  setAge(a => a + 1);
  // ...
```

---

# `useState`
Utilização típica

[Basic useState examples](https://react.dev/reference/react/useState#usage)

---
layout: section
---

# `useEffect`

---
layout: quote
---

# `useEffect`

> Permite realizar ações complementares, tais como buscar dados, atualizar o DOM, disparar *timers*, etc nos componentes.

---

# `useEffect(function, dependency)`

- Roda a cada renderização
- Utiliza dois argumentos
  - `function` define o que será executado
  - `dependency` variável de controle

---

# `useEffect`
Exemplo sem dependência

```js
import { useState, useEffect } from 'react';
import { createRoot } from 'react-dom/client';

function Timer() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    setTimeout(() => {
      setCount((count) => count + 1);
    }, 1000);
  });

  return <h1>I've rendered {count} times!</h1>;
}

createRoot(document.getElementById('root')).render(
  <Timer />
);
```

[Rodar Exemplo](https://www.w3schools.com/react/showreact.asp?filename=demo_react_useeffect_settimeout)

---

# `useEffect`
Exemplo sem dependência
1. `useEffect` roda a cada renderização
2. A cada modificação do contador uma renderização acontece, chamando novamente `useEffect`
3. O contador é modificado novamente e sem limites

> Como controlar quando `useEffect` roda?

---

# `useEffect`
Renderização inicial

```js {11}
import { useState, useEffect } from 'react';
import { createRoot } from 'react-dom/client';

function Timer() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    setTimeout(() => {
      setCount((count) => count + 1);
    }, 1000);
  }, []);

  return <h1>I've rendered {count} times!</h1>;
}

createRoot(document.getElementById('root')).render(
  <Timer />
);
```

[Rodar Exemplo](https://www.w3schools.com/react/showreact.asp?filename=demo_react_useeffect_settimeout2)

---

# `useEffect`
Dependência de uma variável

```js {10}
import { useState, useEffect } from 'react';
import { createRoot } from 'react-dom/client';

function Counter() {
  const [count, setCount] = useState(0);
  const [calculation, setCalculation] = useState(0);

  useEffect(() => {
    setCalculation(() => count * 2);
  }, [count]);

  return (
    <>
      <p>Count: {count}</p>
      <button onClick={() => setCount((c) => c + 1)}>+</button>
      <p>Calculation: {calculation}</p>
    </>
  );
}

createRoot(document.getElementById('root')).render(
  <Counter />
);
```

---
layout: section
---

# `useContext`

---
layout: quote
---

# `useContext`

> O React Context é uma forma de gerenciar o estado **globalmente**. Pode ser usado em conjunto com  `useState` para compartilhar o estado entre componentes aninhados

---

# `useContext`
*Prop drilling*

- O estado deve ser mantido pelo componente pai de nível mais alto na pilha que necessita acessar o estado
- Imagine que temos vários componentes aninhados, logo os componentes no topo e na base da pilha precisam acessar o estado
- Para fazer isso sem usar o Contexto, é necessário passar o estado como `props` através de cada componente aninhado (*prop drilling*)

---

# `useContext`
Exemplo de *Prop drilling*

```js {*}{maxHeight:'400px'}
import { useState } from 'react';
import { createRoot } from 'react-dom/client';

function Component1() {
  const [user, setUser] = useState("Linus");

  return (
    <>
      <h1>{`Hello ${user}!`}</h1>
      <Component2 user={user} />
    </>
  );
}

function Component2({ user }) {
  return (
    <>
      <h1>Component 2</h1>
      <Component3 user={user} />
    </>
  );
}

function Component3({ user }) {
  return (
    <>
      <h1>Component 3</h1>
      <h2>{`Hello ${user} again!`}</h2>
    </>
  );
}

createRoot(document.getElementById('root')).render(
  <Component1 />
);
```

---

# `useContext`
Exemplo com hook

```js {*}{maxHeight:'400px'}
import { useState, createContext, useContext } from 'react';
import { createRoot } from 'react-dom/client';

const UserContext = createContext();

function Component1() {
  const [user, setUser] = useState("Linus");

  return (
    <UserContext.Provider value={user}>
      <h1>{`Hello ${user}!`}</h1>
      <Component2 />
    </UserContext.Provider>
  );
}

function Component2() {
  return (
    <>
      <h1>Component 2</h1>
      <Component3 />
    </>
  );
}

function Component3() {
  const user = useContext(UserContext);

  return (
    <>
      <h1>Component 3</h1>
      <h2>{`Hello ${user} again!`}</h2>
    </>
  );
}

createRoot(document.getElementById('root')).render(
  <Component1 />
);
```

---
layout: section
---

# `useRef`

---
layout: quote
---

# `useRef`

> `useRef` permite persistir valores entre renderizações

---

# `useRef`

- Pode ser usado para armazenar um valor mutável que não causa uma nova renderização quando atualizado
- Para acessar um elemento DOM diretamente
- Retorna o objeto `current`

---

```js 
import { useState, useRef, useEffect } from 'react';
import { createRoot } from 'react-dom/client';

function App() {
  const [inputValue, setInputValue] = useState("");
  const count = useRef(0);

  useEffect(() => {
    count.current = count.current + 1;
  });

  return (
    <>
      <p>Type in the input field:</p>
      <input
        type="text"
        value={inputValue}
        onChange={(e) => setInputValue(e.target.value)}
      />
      <h1>Render Count: {count.current}</h1>
    </>
  );
}

createRoot(document.getElementById('root')).render(
  <App />
);
```

[Rodar Exemplo](https://www.w3schools.com/react/showreact.asp?filename=demo_react_useref)

---

```js
import { useRef } from 'react';
import { createRoot } from 'react-dom/client';

function App() {
  const inputElement = useRef();

  const focusInput = () => {
    inputElement.current.focus();
  };

  return (
    <>
      <input type="text" ref={inputElement} />
      <button onClick={focusInput}>Focus Input</button>
    </>
  );
}

createRoot(document.getElementById('root')).render(
  <App />
);
```

[Rodar Exemplo](https://www.w3schools.com/react/showreact.asp?filename=demo_react_useref2)

---
layout: section
---

# `useReducer`

---
layout: quote
---

# `useReducer`

> Semelhante a `useState`, porém pode aplicar uma lógica mais apurada

---

`useReducer(reducer, initialState, init)`

- `reducer` função com a lógica personalizada
- `initialState` objeto de inialização
- `init` incializa o estado (opcional)

---

# `useReducer`
Exemplo

```js {*}{maxHeight:'400px'}
import { useReducer } from 'react';
import { createRoot } from 'react-dom/client';

const initialScore = [
  {
    id: 1,
    score: 0,
    name: "John",
  },
  {
    id: 2,
    score: 0,
    name: "Sally",
  },
];

const reducer = (state, action) => {
  switch (action.type) {
    case "INCREASE":
      return state.map((player) => {
        if (player.id === action.id) {
          return { ...player, score: player.score + 1 };
        } else {
          return player;
        }
      });
    default:
      return state;
  }
};

function Score() {
  const [score, dispatch] = useReducer(reducer, initialScore);

  const handleIncrease = (player) => {
    dispatch({ type: "INCREASE", id: player.id });
  };

  return (
    <>
      {score.map((player) => (
        <div key={player.id}>
          <label>
            <input
              type="button"
              onClick={() => handleIncrease(player)}
              value={player.name}
            />
            {player.score}
          </label>
        </div>
      ))}
    </>
  );
}

createRoot(document.getElementById('root')).render(
  <Score />
);
```

[Rodar Exemplo](https://www.w3schools.com/react/showreact.asp?filename=demo_react_usereducer)

---
layout: section
---

# `useCallback` e `useMemo`

---
layout: quote
---

# `useMemo`

> Usado para memorizar (armazenar em *cache*) um valor e retornar

---
layout: quote
---

# `useCallback`

> Usado para memorizar uma função de retorno de chamada

---

# `useCallback(callback, dependencies)`

- `callback` função a ser armazenada
- `dependencies` um array contendo variáveis de dependências. Caso uma das dependências mude, a função `callback` é executada novamente

---

# Sem `useCallback`

```js {*}{maxHeight: '400px'}
import React, { useState } from 'react';
import { createRoot } from 'react-dom/client';

// Child component that receives a function prop
const Button = React.memo(({ onClick, text }) => {
  alert(`Child ${text} button rendered`);
  return <button onClick={onClick}>{text}</button>;
});

// Parent component without useCallback
function WithoutCallbackExample() {
  const [count1, setCount1] = useState(0);
  const [count2, setCount2] = useState(0);

  // This function is recreated on every render
  const handleClick1 = () => {
    setCount1(count1 + 1);
  };

  const handleClick2 = () => {
    setCount2(count2 + 1);
  };

  alert('Parent rendered');
  return (
    <div>
      <h2>Without useCallback:</h2>
      <p>Count 1: {count1}</p>
      <p>Count 2: {count2}</p>
      <Button onClick={handleClick1} text="Button 1" />
      <Button onClick={handleClick2} text="Button 2" />
    </div>
  );
}

createRoot(document.getElementById('root')).render(<WithoutCallbackExample />);
```

---

# Aplicando `useCallback`

```js {*}{maxHeight: '400px'}
import React, { useState, useCallback } from 'react';
import { createRoot } from 'react-dom/client';

// Child component that receives a function prop
const Button = React.memo(({ onClick, text }) => {
  console.log(`${text} button rendered`);
  return <button onClick={onClick}>{text}</button>;
});

// Parent component with useCallback
function WithCallbackExample() {
  const [count1, setCount1] = useState(0);
  const [count2, setCount2] = useState(0);

  // These functions are memoized and only recreated when dependencies change
  const handleClick1 = useCallback(() => {
    setCount1(count1 + 1);
  }, [count1]);

  const handleClick2 = useCallback(() => {
    setCount2(count2 + 1);
  }, [count2]);

  console.log("Parent rendered");
  return (
    <div>
      <h2>With useCallback:</h2>
      <p>Count 1: {count1}</p>
      <p>Count 2: {count2}</p>
      <Button onClick={handleClick1} text="Button 1" />
      <Button onClick={handleClick2} text="Button 2" />
    </div>
  );
}

createRoot(document.getElementById('root')).render(
  <WithCallbackExample />
); 
```

---
layout: section
---

# `useMemo`

---

# `useMemo`

> Pode ser usado para evitar que funções dispendiosas e que consomem muitos recursos sejam executadas desnecessariamente.

---

# Sem `useMemo`

```js {*}{maxHeight: '400px'}
import { useState } from 'react';
import { createRoot } from 'react-dom/client';


const App = () => {
  const [count, setCount] = useState(0);
  const [todos, setTodos] = useState([]);
  const calculation = expensiveCalculation(count);

  const increment = () => {
    setCount((c) => c + 1);
  };
  const addTodo = () => {
    setTodos((t) => [...t, "New Todo"]);
  };

  return (
    <div>
      <div>
        <h2>My Todos</h2>
        {todos.map((todo, index) => {
          return <p key={index}>{todo}</p>;
        })}
        <button onClick={addTodo}>Add Todo</button>
      </div>
      <hr />
      <div>
        Count: {count}
        <button onClick={increment}>+</button>
        <h2>Expensive Calculation</h2>
        {calculation}
        <p>Note that this example executes the expensive function also when you click on the Add Todo button.</p>
      </div>
    </div>
  );
};

const expensiveCalculation = (num) => {
  console.log("Calculating...");
  for (let i = 0; i < 1000000000; i++) {
    num += 1;
  }
  return num;
};

createRoot(document.getElementById('root')).render(
  <App />
);
```

[Rodar Exemplo](https://www.w3schools.com/react/showreact.asp?filename=demo_react_usememo_without)

---

# Aplicando `useMemo`

```js {*}{maxHeight: '400px'}
import { useState, useMemo } from 'react';
import { createRoot } from 'react-dom/client';

const App = () => {
  const [count, setCount] = useState(0);
  const [todos, setTodos] = useState([]);
  const calculation = useMemo(() => expensiveCalculation(count), [count]);

  const increment = () => {
    setCount((c) => c + 1);
  };
  const addTodo = () => {
    setTodos((t) => [...t, "New Todo"]);
  };

  return (
    <div>
      <div>
        <h2>My Todos</h2>
        {todos.map((todo, index) => {
          return <p key={index}>{todo}</p>;
        })}
        <button onClick={addTodo}>Add Todo</button>
      </div>
      <hr />
      <div>
        Count: {count}
        <button onClick={increment}>+</button>
        <h2>Expensive Calculation</h2>
        {calculation}
        <p>Note: This example executes the expensive function only when you click on the Increment button, and not when you add a todo.</p>
      </div>
    </div>
  );
};

const expensiveCalculation = (num) => {
  console.log("Calculating...");
  for (let i = 0; i < 1000000000; i++) {
    num += 1;
  }
  return num;
};

createRoot(document.getElementById('root')).render(
  <App />
);
```

[Rodar Exemplo](https://www.w3schools.com/react/showreact.asp?filename=demo_react_usememo_with)

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
Criar um Blog Pessoal utilizando React. Preencha o conteúdo com dados "fake" gerados por APIS como JSONPlaceholder ou similar.
<!-- **Nível:** Intermediário | **Tempo:** 15 horas -->

Criar um blog com as funcionalidades:
- Página inicial com lista de artigos
- Página de artigo individual
- Página sobre
- Formulário de contato
- Componentes reutilizáveis
- Dados em JSON ou API (JSONPlaceholder)
- Responsividade

---

# Referências

- [Bulit-in React Hooks](https://react.dev/reference/react/hooks)
- [W3Schools React Hooks](https://www.w3schools.com/react/react_hooks.asp)
- [JSONPlaceholder](https://jsonplaceholder.typicode.com/guide/)

---
src: /snippets/end.md
---