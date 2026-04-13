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
exportFilename: pw2_aula7_eventos
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
- Hooks personalisadas

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
    - O estado atual. Durante a primeira renderização, ele corresponderá ao `initialState` que você passado
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

---

# Referências

- [Bulit-in React Hooks](https://react.dev/reference/react/hooks)
- [W3Schools React Hooks](https://www.w3schools.com/react/react_hooks.asp)

---
src: /snippets/end.md
---