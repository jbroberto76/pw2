---
theme: default
transition: fade
colorSchema: dark
lineNumbers: true
layout: image
image: /cover.svg
description: Programação Web 2
author: José Roberto Bezerra
title: Introdução JSX
exportFilename: pw2_aula5_jsx
---

# JSX
JavaScript XML for React

---

# O que é JSX?
JavaScript XML
- Permite escrever sintaxe HTML diretamente em JavaScript
- Facilita a escrita e adição de HTML no React
- É traduzido para JavaScript em tempo de execução
- Baseado na extensão ES6

---

# Por que JSX?
Limpo e melhor legibilidade

JSX
```js {*}{class: '!children:text-xl'}
const myElement = <h1>I Love JSX!</h1>;

createRoot(document.getElementById('root')).render(
  myElement
```

JS
```js {*}{class: '!children:text-xl'}
const myElement = React.createElement('h1', {}, 'I do not use JSX!');

createRoot(document.getElementById('root')).render(
  myElement
```

---

# JSX is HTML-like
JSX converte tags HTML em elementos React

```js {*}{class: '!children:text-xl'}
const myElement = <h1>Hello React!</h1>;

createRoot(document.getElementById('root')).render(myElement);
```

- Não necessita `createElement()` ou `appendChild()`
- HTML inserido diretamente no JS

---

# Expressões em JSX
Uso de `{ }`

```js {*}{class: '!children:text-xl'}
const myElement = <h1>React is {5 + 5} times better with JSX</h1>;
```

Expressões válidas:
- Variáveis
- Propriedades
- Expressões JS

---

# HTML Multi linhas
Uso de `( )`

```js
const myElement = (
  <ul>
    <li>Apples</li>
    <li>Bananas</li>
    <li>Cherries</li>
  </ul>
);
```

---

# One Top Level Element
Tag única

```js {*}{class: '!children:text-xl'}
// - Correct - wrapped in div
const myElement = (
  <div>
    <p>I am a paragraph.</p>
    <p>I am a paragraph too.</p>
  </div>
);
```

> Sem um elemento pai, o JSX gera um erro!

---

# Fragmentos
Uso de `<></>`

```js {*}{class: '!children:text-xl'}
const myElement = (
  <>
    <p>I am a paragraph.</p>
    <p>I am a paragraph too.</p>
  </>
);
```

> Alternativa mais limpa do que utilizar uma `<div>` extra

---

# Elementos Fechados
Fechamento obrigatório de tags

```js {*}{class: '!children:text-xl'}
// - Correct
const myElement = <input type="text" />;

// ✗ Wrong
const myElement = <input type="text">;
```

> JSX gera um erro se os elementos não forem fechados corretamente

---

# `className`

- O atributo `class` é uma palavra reservada JS

```js {*}{class: '!children:text-xl'}
const myElement = <h1 className="myclass">Hello World</h1>;
```

> JSX traduz `className` em atributos `class` quando renderizado.

---

# Comentários
`{/* */}`:

```js {*}{class: '!children:text-xl'}
const myElement = <h1>Hello {/* Wonderful */} World</h1>;
```

> Os comentários devem estar dentro de chaves no JSX.

---
layout: section
---

# Componentes

---

# JSX em Componentes
- O React usa componentes para construir interfaces de usuário
- Os componentes são trechos de código independentes e reutilizáveis
- São como funções JavaScript e retornam HTML
- O JSX funciona perfeitamente dentro dos componentes do React

---

# JSX em Componentes
Exemplo

```js {*}{class: '!children:text-xl'}
function Car() {
  return (
    <>
      <h2>My Car</h2>
      <p>It is a Ford Mustang.</p>
    </>
  );
}

createRoot(document.getElementById('root')).render(<Car />);
```

---

# JSX em Componentes
Realizando operações

```js {all|2,3}{class: '!children:text-xl'}
function Car() {
  const brand = "Ford";
  const model = "Mustang";
  
  return (
    <>
      <h2>My Car</h2>
      <p>It is a {brand} {model}.</p>
    </>
  );
}
```

> Combina a lógica JavaScript com a marcação de forma integrada.

---

# Resumo JSX

- JSX torna o código React mais legível e natural
- JSX parece HTML, mas na verdade é JavaScript
- Expressões devem ser colocadas dentro de chaves `{ }`
- Sempre envolva JSX com várias linhas entre parênteses
- Use um elemento (ou fragmentos) de nível superior
- Todos os elementos devem ser autofechados ou fechados corretamente
- Use `className` em vez de `class`
- JSX funciona perfeitamente em componentes React

---

# Expressões JSX

> JSX permite incorporar **qualquer expressão JavaScript válida** dentro da marcação.

- Envolva expressões em chaves `{ }`
- O React avalia a expressão e renderiza o resultado
- Torna o JSX dinâmico e poderoso

---

# Expressões JSX
Exemplo

```js {*}{class: '!children:text-xl'}
function Car() {
  return (
    <>
      <h1>My car</h1>
      <p>It has {218 * 1.36} horsepower</p>
    </>
  );
}
```

---

# Usando Variáveis

```js {*|2,6}{class: '!children:text-xl'}
function Car() {
  const hp = 218 * 1.36;
  return (
    <>
      <h1>My car</h1>
      <p>It has {hp} horsepower</p>
    </>
  );
}
```

> Defina variáveis ​​fora do JSX e faça referência a elas dentro de `{ }`.

---

# Chamadas de Função

```js {*|9}{class: '!children:text-xl'}
function kwtohp(kw) {
  return kw * 1.36;
}

function Car() {
  return (
    <>
      <h1>My car</h1>
      <p>It has {kwtohp(218)} horsepower</p>
    </>
  );
}
```

> As funções retornam valores que são renderizados.

---

# Propriedades de Objetos
*dot notation*

```js {*|10}{class: '!children:text-sm'}
function Car() {
  const myobj = {
    name: "Fiat",
    model: "500",
    color: "white"
  };
  
  return (
    <>
      <h1>My car is a {myobj.color} {myobj.name} {myobj.model}</h1>
    </>
  );
}
```

> Combine várias propriedades em uma única expressão JSX.

---

# Expressões em JSX
Resumo
- Qualquer expressão JavaScript válida funciona
- Deve estar entre chaves `{ }`
- É avaliada no momento da renderização
- Pode incluir variáveis, chamadas de função e propriedades de objetos
- O resultado é inserido no DOM

---

# Expressões em JSX
Usos típicos
- Cálculos matemáticos
- Concatenação de strings
- Renderização condicional (tópicos posteriores)
- Mapeamento de arrays (tópicos posteriores)
- Formatação de valores
- Geração de conteúdo dinâmico

---
layout: section
---

# Atributos JSX

---

# `class` versus `className`

> In JSX, `class` is a reserved JavaScript keyword

```js {*|3}{class: '!children:text-xl'}
function Car() {
  return (
    <h1 className="myclass">Hello World</h1>
  );
}
```

---

# Expressões como atributos

> Pode-se utilizar expressões JS para valores de atributos dinâmicos

```js {*|4}{class: '!children:text-xl'}
function Car() {
  const x = "myclass";
  return (
    <h1 className={x}>Hello World</h1>
  );
}
```

- Envolver expressões em chaves `{ }`
- Não utilizar aspas
- Perfeito para estilização e comportamento dinâmicos

---

# Atributos de Eventos em *camelCase*

```js {*|7}{class: '!children:text-xl'}
function Car() {
  const myfunc = () => {
    alert('Hello World');
  };
  
  return (
    <button onClick={myfunc}>Click me</button>
  );
}
```

- `onClick` ao invés de `onclick`
- `onMouseOver` ao invés de `onmouseover`
- Segue a convenção de nomes do JS

---

# Atributos Boleanos
Diferente em JSX

```js {*}{class: '!children:text-xl'}
// This makes the button disabled
<button onClick={myfunc} disabled>Click me</button>

// Also disabled
<button onClick={myfunc} disabled={true}>Click me</button>

// NOT disabled
<button onClick={myfunc} disabled={false}>Click me</button>
```

> Presença do atributo implica `true`
<!-- - `disabled={false}` explicitly sets to false
- Use expressions for dynamic boolean values -->

---

# Atributo `style`

> Atributos de estilo aceitam objetos JavaScript com propriedades em camelCase

```js {*}{class: '!children:text-sm'}
function Car() {
  const mystyles = {
    color: "red",     fontSize: "20px",     backgroundColor: "lightyellow",
  };
  return (
    <>
      <h1 style={mystyles}>My car</h1>
    </>
  );
}
```

- Objeto com propriedades CSS em camelCase
- `fontSize` em vez de `font-size`, `backgroundColor` em vez de `background-color`

---

# Regras de estilo para objetos
Diferenças entre HTML e CSS

- Propriedades em camelCase
- Valores como *strings*
- Sem seletores CSS (apenas estilos inline)
- Permite o uso de variáveis ​​e expressões

```js {*}{class: '!children:text-xl'}
const buttonStyle = {
  backgroundColor: 'blue',
  color: 'white',
  padding: '10px 20px',
  borderRadius: '5px'
};
```

---

# Padrões Comuns para Atributos

- `className` para classes CSS
- `onClick`, `onChange`, etc para eventos
- `style` para estilos *inline*
- `disabled`, `checked` para boleanos
- Usar `{ }` para valores dinâmicos

---
layout: section
---

# Condicionais

---

# Renderização Condicional em JSX

> React não permite instruções `if` diretamente dentro do JSX.

Há duas abordagens a seguir:

1. Escrever instruções `if` fora do JSX
2. Usar expressões ternárias dentro do JSX

---

# Renderização Condicional em JSX
`if` fora do JSX

> Utilizar a lógica antes de `return`

```js {*|2-6}{class: '!children:text-sm'}
function Fruit() {
  const x = 5;
  let y = "Apple";
  if (x < 10) {
    y = "Banana";
  }
  return (
    <h1>{y}</h1>
  );
}
```

- A lógica ocorre antes do JSX
- A variável contém o resultado
- Código limpo e legível

---

# Renderização Condicional em JSX
Expressões ternárias

```js {*}{class: '!children:text-xl'}
function Fruit() {
  const x = 5;
  
  return (
    <h1>{(x) < 10 ? "Banana" : "Apple"}</h1>
  );
}
```

- Condição ? valor_verdadeiro : valor_falso
- Deve estar entre chaves `{ }`
- Perfeito para condições simples

---

# Operador Ternário
Sintaxe

```js {*}{class: '!children:text-xl'}
condition ? expression_if_true : expression_if_false
```

- `condition`: expressão boleana
- `?`: Executado quando `true`
- `:`: Executado quando `false`

---
layout: two-cols-header
---

# Quando Usar Cada Abordagem?

:: left ::

**`if` fora do JSX**
- A lógica for complexa
- Houver múltiplas condições
- For necessário definir múltiplas variáveis
- Estrutura de componente mais limpa

:: right ::

**Expressões ternárias**
- Houver condições simples de verdadeiro/falso
- Houver renderização condicional embutida
- Houver expressões curtas e legíveis

---

# Outros Casos
Múltiplos `if-else`

```js {*}{class: '!children:text-xl'}
function StatusMessage({ status }) {
  let message;
  
  if (status === 'loading') {
    message = 'Loading...';
  } else if (status === 'success') {
    message = 'Success!';
  } else {
    message = 'Error occurred';
  }

  return <p>{message}</p>;
}
```

---

# Outros Casos
Ternários Aninhados

```js {*}{class: '!children:text-xl'}
// Readable
{isLoggedIn ? 'Welcome!' : 'Please log in'}

// Less readable - avoid if possible
{status === 'loading' ? 'Loading...' : 
 status === 'success' ? 'Done!' : 'Error'}
```

---

# Boas Práticas

- Mantenha as condições simples e legíveis
- Use instruções `if` para lógica complexa
- Use operadores ternários para condições simples em linha
- Considere extrair lógica complexa para funções
- Teste todos os ramos condicionais

---

# Resumo
Condicionais

> A renderização condicional torna os componentes dinâmicos

- As instruções `if` devem estar fora do JSX
- Os operadores ternários funcionam dentro de `{ }`
- Escolha a abordagem com base na complexidade
- Sempre teste os casos verdadeiro e falso
- Mantenha o código legível e de fácil manutenção

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
Realizar o Quiz 


---

# Referências

- [Introdução JSX](https://www.w3schools.com/react/react_jsx.asp) 
- [React](https://react.dev/)

---
src: /snippets/end.md
---
