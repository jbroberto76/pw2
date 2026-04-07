---
theme: default
transition: fade
colorSchema: dark
lineNumbers: true
layout: image
image: /cover.svg
description: Programação Web 2
author: José Roberto Bezerra
title: Componentes React
exportFilename: pw2_aula6_componentes
---

# {{ $slidev.configs.title }}
{{ $slidev.configs.description }}

---

# Objetivo de Aprendizagem
- Conhecer, criar e utilizar componentes React

---

# Agenda

- O que são componentes React
- Funções vs Classes
- Props e passagem de dados
- Desestruturação de Props
- Props.children
- Exemplos práticos

---

# Componentes React?

> São fragmentos independentes e reutilizáveis de código que tem o mesmo propósito que funções JS. Retornam elementos HTML através de uma função ou método *render*

```js {*}{class: '!children:text-xl'}
function Car() {
  return (
    <h2>Eu sou um carro!</h2>
  );
}
```

---

# Tipos de Componentes

1. Function Components
2. Class Components

---

# Tipos de Componentes

1. **Function Components** (Recomendado)
- Componentes criados como funções JavaScript
- Simples e diretos
- Suportam *Hooks*

---

# Tipos de Componentes

2. **Class Components**
- Componentes criados como classes que estendem `React.Component`
- Mais complexos
- Usados em código legado

---

# Regras Importantes

- Nome deve começar com LETRA MAIÚSCULA
    - `<Car />` ✓
    - `<car />` ✗

- Retornam HTML usando JSX
- Podem ser reutilizados

```js {*}{class: '!children:text-xl'}
function Car() {
  return <h2>Eu sou um carro!</h2>;
}

createRoot(document.getElementById('root')).render(<Car />);
```

---

# Class Components
Criando um componente de classe

```js {*}{class: '!children:text-xl'}
class Car extends React.Component {
  render() {
    return <h2>Oi, eu sou um Carro!</h2>;
  }
}
```

Um componente de classe:
- Estende `React.Component`
- Possui um método `render()` obrigatório
- O método `render()` retorna HTML

---

# Class Components 
Constructor

> O constructor é chamado antes de qualquer outra coisa

```js {*}{class:'!children:text-xl'}
class Car extends React.Component {
  constructor(props) {
    super(props);
    this.state = { color: "red" };
  }
  
  render() {
    return <h2>Eu sou um carro {this.state.color}!</h2>;
  }
}
```

---

# Class Components 
Constructor

- Use `super(props)` para herdar as funções do `React.Component`
- Inicialize o `state` no constructor

---

# Componentes dentro de Componentes

> Componentes podem ser usados dentro de outros componentes:

```js {*}{class:'!children:text-sm'}
function Car() {
  return <h2>Eu sou um Carro!</h2>;
}
function Garage() {
  return (
    <>
      <h1>Quem mora em minha garagem?</h1>
      <Car />
    </>
  );
}
createRoot(document.getElementById('root')).render(<Garage />);
```

---

# Componentes em Arquivos Separados

> Organizar os componentes em arquivos separados (`.jsx`)

`vehicle.jsx`
```javascript
import React from 'react';

function Car() {
  return <h2>Oi, eu sou um Carro!</h2>;
}

export default Car;
```

`App.jsx`
```javascript
import Car from './Vehicle.jsx';

createRoot(document.getElementById('root')).render(<Car />);
```

---

# Props

> Props são como argumentos de função em JavaScript e atributos em HTML

```js {*}{class:'!children:text-sm'}
function Car(props) {
  return <h2>Eu sou um {props.color} Carro!</h2>;
}

createRoot(document.getElementById('root')).render(
  <Car color="red" />
);
```

- Props são **read-only**
- Passadas como atributos no JSX
- Acessadas via `props.nomeDaPropriedade`

---

# Props
Múltiplas Propriedades

```js {*}{class:'!children:text-xl'}
function Car(props) {
  return (
    <h2>Eu sou um {props.color} {props.brand} {props.model}!</h2>
  );
}

createRoot(document.getElementById('root')).render(
  <Car brand="Ford" model="Mustang" color="red" />
);
```

> Cada atributo se torna uma propriedade no objeto `props`

---

# Props
Diferentes Tipos de Dados

```js {*}{class:'!children:text-xl'}
// Strings - aspas normais
<Car brand="Ford" />

// Números - chaves {}
<Car year={1969} />

// Variáveis - chaves {}
let x = "Ford";
<Car brand={x} />

// Objetos e Arrays - chaves {}
let carInfo = { name: "Ford", model: "Mustang" };
<Car carinfo={carInfo} />
```

---

# Props
Acessando Objetos

```js {*}{class:'!children:text-xl'}
function Car(props) {
  return (
    <>
      <h2>Meu {props.carinfo.name} {props.carinfo.model}!</h2>
      <p>Cor: {props.carinfo.color}</p>
    </>
  );
}
```

---

# Props
Acessando Arrays

```js {*}{class:'!children:text-xl'}
function Car(props) {
  return (
    <h2>Meu carro é um {props.carinfo[0]} {props.carinfo[1]}!</h2>
  );
}
```

---

# Props
Parâmetros entre Componentes

```javascript
function Car(props) {
  return <h2>Eu sou um {props.brand}!</h2>;
}

function Garage() {
  return (
    <>
      <h1>Quem mora em minha garagem?</h1>
      <Car brand="Ford" />
    </>
  );
}

createRoot(document.getElementById('root')).render(<Garage />);
```

---

# Desestruturação de Props

> Visa simplificar o código desestruturando o que for necessário

```js {*}{class:'!children:text-sm'}
// Sem desestruturação
function Car(props) {
  return <h2>Meu carro é {props.color}!</h2>;
}

// Com desestruturação - no parâmetro
function Car({color}) {
  return <h2>Meu carro é {color}!</h2>;
}

// Com desestruturação - no corpo da função
function Car(props) {
  const {brand, model} = props;
  return <h2>Eu amo meu {brand} {model}!</h2>;
}
```

---

# Desestruturação
Rest Operator

> Utilizar `...rest` quando a quantidade `props` é desconhecida

```js {*}{class:'!children:text-sm'}
function Car({color, brand, ...rest}) {
  return (
    <h2>Meu {brand} {rest.model} é {color}!</h2>
  );
}
<Car 
  brand="Ford" 
  model="Mustang" 
  color="red" 
  year={1969} 
/>
```

- Nesse exemplo `rest` armazena: `{ model: "Mustang", year: 1969 }`

---

# Desestruturação
Valores Padrão

> É possível configurar valores padrão para `props``

```js {*}{class:'!children:text-sm'}
function Car({color = "blue", brand}) {
  return (
    <h2>Meu {color} {brand}!</h2>
  );
}

<Car brand="Ford" />
```

- Se a `prop` não for fornecida, o valor padrão é utilizado

---

# `Props.children`

> Utilizar `props.children` para enviar com conteúdo entre tags de abertura e fechamento ([ver exemplo](https://www.w3schools.com/react/showreact.asp?filename=demo_react_props_children))

---

```js {*}
function Son(props) {
  return (
    <div style={{background: 'lightgreen'}}>
      <h2>Son</h2>
      <div>{props.children}</div>
    </div>
  );
}
function Daughter(props) {
  const {brand, model} = props;
  return (
    <div style={{background: 'lightblue'}}>
      <h2>Daughter</h2>
      <div>{props.children}</div>
    </div>
  );
}
function Parent() {
  return (
    <div>
      <h1>My two Children</h1>
      <Son>
        <p>
          This was written in the Parent component,
          but displayed as a part of the Son component
        </p>
      </Son>
      <Daughter>
        <p>
          This was written in the Parent component,
          but displayed as a part of the Daughter component
        </p>
      </Daughter>
    </div>
  );
}
```

---

# Props.children
Múltiplos Componentes

```javascript
function Daughter(props) {
  return (
    <div style={{background: 'lightblue'}}>
      <h2>Filha</h2>
      <div>{props.children}</div>
    </div>
  );
}

function Parent() {
  return (
    <>
      <Son>
        <p>Conteúdo do Filho</p>
      </Son>
      <Daughter>
        <p>Conteúdo da Filha</p>
      </Daughter>
    </>
  );
}
```

---

# State vs Props

| Aspecto | Props | State |
|--------|-------|-------|
| **Origem** | Recebidas como parâmetros | Definidas no próprio componente |
| **Leitura** | Read-only (imutável) | Pode ser alterado |
| **Use para** | Passar dados entre componentes | Dados que mudam |
| **Atualização** | Não pode ser alterada | `setState()` em classes |

---

# State em Class Components

```js {*}{class:'!children:text-sm'}
class Car extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      brand: "Ford",
      color: "red",
      year: 1964
    };
  }
  
  render() {
    return (
      <>
        <h1>Meu {this.state.brand}</h1>
        <p>Cor: {this.state.color}, Ano: {this.state.year}</p>
      </>
    );
  }
}
```

---

# Alterando State em Class Components

```javascript
class Car extends React.Component {
  constructor(props) {
    super(props);
    this.state = { color: "red" };
  }
  
  changeColor = () => {
    this.setState({ color: "blue" });
  }
  
  render() {
    return (
      <>
        <h2>Meu carro é {this.state.color}</h2>
        <button onClick={this.changeColor}>Mudar Cor</button>
      </>
    );
  }
}
```

- Use `setState()` para atualizar state, não faça atribuição direta!

---

# Exemplo 1
Card de Produto

```js {*}{class:'!children:text-sm'}
function ProductCard({name, price, image, children}) {
  return (
    <div style={{border: '1px solid #ccc', padding: '10px'}}>
      <img src={image} alt={name} />
      <h3>{name}</h3>
      <p>R$ {price}</p>
      <div>{children}</div>
    </div>
  );
}

// Uso
<ProductCard 
  name="Notebook" 
  price="2999.99"
  image="notebook.jpg"
>
  <button>Comprar</button>
</ProductCard>
```

---

# Exemplo 2
Lista de Itens

```javascript
function Item({title, completed}) {
  return (
    <li style={{
      textDecoration: completed ? 'line-through' : 'none'
    }}>
      {title}
    </li>
  );
}

function ItemList({items}) {
  return (
    <ul>
      {items.map((item, index) => (
        <Item key={index} title={item.title} completed={item.completed} />
      ))}
    </ul>
  );
}
```

---

# Boas práticas

- Use nomes auto-descritivos para props  
- Desestruture props quando possível  
- Mantenha componentes simples
- Reutilize componentes o máximo possível  
- Utilizar `Props.children` para composição  
- Evitar props muito aninhadas (prop drilling)

---

# Exemplo 3
Componente de Botão

```javascript
function Button({text, onClick, color = "blue"}) {
  return (
    <button
      onClick={onClick}
      style={{
        backgroundColor: color,
        color: 'white',
        padding: '10px 20px',
        border: 'none',
        borderRadius: '4px',
        cursor: 'pointer'
      }}
    >
      {text}
    </button>
  );
}

// Uso
<Button text="Clique aqui" color="green" onClick={() => alert('Clicado!')} />
```

---

# Exemplo 4
Componente de Card

```javascript
function Card({title, description, footer}) {
  return (
    <div style={{
      border: '1px solid #ddd',
      borderRadius: '8px',
      padding: '16px',
      marginBottom: '16px',
      boxShadow: '0 2px 8px rgba(0,0,0,0.1)'
    }}>
      <h2>{title}</h2>
      <p>{description}</p>
      {footer && <footer>{footer}</footer>}
    </div>
  );
}

// Uso
<Card 
  title="Bem-vindo" 
  description="Este é um componente de card"
  footer="Rodapé do card"
/>
```

---

# Exemplo 5
Componente com Composição

```javascript
function Container({title, children}) {
  return (
    <div style={{
      maxWidth: '600px',
      margin: '0 auto',
      padding: '20px',
      backgroundColor: '#f5f5f5'
    }}>
      {title && <h1>{title}</h1>}
      <div>{children}</div>
    </div>
  );
}

// Uso
<Container title="Meu Conteúdo">
  <p>Conteúdo dentro do container</p>
  <Button text="Enviar" />
</Container>
```

---
layout: fact
---

# Perguntas?

---
layout: fact
---

# Exercícios

---

# 1
Criar um componente `Greeting` que:
- Aceita uma prop `name`
- Retorna `<h1>Olá, {name}!</h1>`
- Use-o para saudar 3 pessoas diferentes

<!-- 
```javascript
// Sua solução aqui
function Greeting({name}) {
  // ...
}

// Teste com:
// <Greeting name="João" />
// <Greeting name="Maria" />
// <Greeting name="Pedro" />
``` 
-->

---

# 2
Criar um componente `PersonCard` que:
- Aceita props: `name`, `age`, `city`
- Exibe as informações formatadas
- Use desestruturação de props

<!-- 
```javascript
// Sua solução aqui
function PersonCard({name, age, city}) {
  // ...
}

// Teste com:
// <PersonCard name="Ana" age={28} city="São Paulo" />
``` 
-->

---

# 3 (`prop.children`)
Criar um componente `Alert` que:
- Aceita uma prop `type` ("success", "error", "warning")
- Usa `props.children` para o conteúdo
- Muda a cor de fundo baseado no tipo

<!--
```javascript
// Sua solução aqui
function Alert({type, children}) {
  // Define cores por tipo
  // ...
}

// Teste com:
// <Alert type="success">Operação realizada com sucesso!</Alert>
// <Alert type="error">Ocorreu um erro</Alert>
```
-->

---

# 4 (Componente de Lista)

Crie um componente `TodoList` que:
- Aceita uma prop `items` (array de objetos)
- Cada item tem `id` e `text`
- Renderiza como lista `<li>`

```javascript
// Sua solução aqui
function TodoList({items}) {
  // Use map para renderizar
  // ...
}

// Teste com:
const todos = [
  {id: 1, text: "Aprender React"},
  {id: 2, text: "Criar componentes"},
  {id: 3, text: "Dominar Props"}
];
// <TodoList items={todos} />
```

---

# 5 (Componente de Formulário)
Criar um componente `FormInput` que:
- Aceita props: `label`, `type`, `placeholder`, `value`, `onChange`
- Renderiza um label e um input
- Use desestruturação com `...rest` para aceitar outras props do input

<!-- 
```javascript
// Sua solução aqui
function FormInput({label, ...rest}) {
  // ...
}

// Teste com:
// <FormInput label="Nome" type="text" placeholder="Digite seu nome" />
// <FormInput label="Email" type="email" placeholder="seu@email.com" />
``` 
-->

---

# Referências

- [React Documentation](https://react.dev)
- [W3Schools React Components](https://www.w3schools.com/react/react_components.asp)
- [React DevTools](https://react-devtools-tutorial.vercel.app/)

---
src: /snippets/end.md
---