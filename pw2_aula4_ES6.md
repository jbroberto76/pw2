---
theme: default
transition: fade
colorSchema: dark
lineNumbers: true
layout: image
image: /cover.svg
description: Programação Web 2
author: José Roberto Bezerra
title: ECMA Script 6
exportFilename: pw2_aula4_ES6
---

# {{ $slidev.configs.title }}
{{ $slidev.configs.description }}

---

# Objetivo de Aprendizagem
- Revisar a sintaxe padrão ES6

---

# Agenda
- ECMA Script 6
- Sintaxe

---
layout: section
---

# ECMASript 6

---
layout: quote
---

# O que é ES6?

> ECMAScript 6 (ES6/ES2015) é a sexta versão do JavaScript

---

# ES6
Por que?

- Código mais limpo e legível
- Sintaxe compatível com JSX
- Recursos que facilitam a criação de componentes
- **Código React moderno usa ES6**

---
layout: section
---

# Sintaxe ES6

---
layout: two-cols-header
---

# Declaração de Variáveis
`var`
> Antes do ES6 `var` era a forma padrão de declaração de variáveis. Deve ser evitado no ES6.

> `var` define um escopo global para uma variável 

:: left ::

```js
for (var i = 0; i < 5; i++) {
	console.log("Inside the loop:", i);
}
console.log("Outside the loop:", i);
```

:: right ::

```bash
Inside the loop: 0 
Inside the loop: 1 
Inside the loop: 2 
Inside the loop: 3 
Inside the loop: 4 
Outside the loop: 5
```

---

# Declaração de Variáveis
`var`
- Permite que uma variável seja reatribuída

```js
var counter = 10;
var counter;
console.log(counter); // 10
```

---

# Declaração de Variáveis
`let`

> Define um escopo de bloco para uma variável. Declaração padrão do ES6.

```js
let x = 10;
if (x == 10) {
    let x = 20;
    console.log(x); // 20:  reference x inside the block
}
console.log(x); // 10: reference at the begining of the script
```

---
layout: two-cols-header
---

# Declaração de Variáveis
`let`

> Não é possível redeclarar uma variável declarada orinalmente com `let`

:: left ::

```js
let counter = 0;
let counter;
console.log(counter);
```

:: right ::

```bash
Uncaught SyntaxError: Identifier 'counter' has already been declared
```

---

# Declaração de Variáveis
`const`

> Declara um tipo imutável, apenas de leitura. Não é possível fazer uma reatribuição de valor.

```js
const RATE = 0.1;
RATE = 0.2; // TypeError
```

---

# Declaração de Variáveis
`const`

> A inicialização é obrigatória

```js
const RED; // SyntaxError
```

---
layout: two-cols-header
---

# Arrow Functions

> AFs foram disponibilizadas no ES6 como uma formato mais compacto para escrita de funções

:: left ::

```js
let add = function (x, y) {
  return x + y;
};

console.log(add(10, 20)); // 30
```

:: right ::

```js
let add = (x, y) => x + y;

console.log(add(10, 20)); // 30;
```

---

# Arrow Functions

> Quando blocos `{}` são utilizados, `return` é obrigratório

```js
let add = (x, y) => {
  return x + y;
};
```

---

# Arrow Functions
Exemplo com React

```js {all|1-3|5-7|9-15|all}
// Componente funcional (padrão moderno)
const Botao = ({ texto, onClick }) => {
  return <button onClick={onClick}>{texto}</button>
}
// Callback inline
<button onClick={() => console.log('clicou')}>
  Clique
</button>
// Mapeando listas
const Lista = ({ itens }) => (
  <ul>
    {itens.map(item => (
      <li key={item.id}>{item.nome}</li>
    ))}
  </ul>
)
```

---

# Template Strings
Exemplo

```js
const nome = "Maria"
const idade = 28

// Antes (concatenação)
console.log("Meu nome é " + nome + " e tenho " + idade + " anos.")

// Com template string (ES6)
console.log(`Meu nome é ${nome} e tenho ${idade} anos.`)
```

---

# Template Strings
Exemplo com React

```js {all|3|4-6|7-10|all}
const Card = ({ titulo, descricao }) => {
  // Classes dinâmicas
  const classeCSS = `card card-${titulo.toLowerCase()}`
  
  // Conteúdo dinâmico
  return (
    <div className={classeCSS}>
      <h3>{`Título: ${titulo}`}</h3>
      <p>{descricao}</p>
      <span>{`Última atualização: ${new Date().toLocaleDateString()}`}</span>
    </div>
  )

// CSS-in-JS com template strings
const estilo = `
  background: linear-gradient(45deg, ${cor1}, ${cor2});
  padding: ${espacamento}px;
`
```

---

# Destructuring 
Desestruturação

> Extrair valores de objetos e arrays de forma elegante

```js {1|2-3|all}
// Sem destructuring
const Usuario = (props) => {
  return <h1>{props.nome} - {props.email}</h1>
}

// Com destructuring (mais comum em React)
const Usuario = ({ nome, email }) => {
  return <h1>{nome} - {email}</h1>
}
```

---

# Destructuring
Exemplo

```js {all|2|3|5-8|all}
const Exemplo = () => {
  // Destructuring em hooks
  const [usuario, setUsuario] = useState(null)
  
  // Destructuring em objetos retornados
  useEffect(() => {
    fetch('/api/usuario')
      .then(res => res.json())
      .then(({ nome, email, endereco: { cidade } }) => {
        // Extraímos nome, email e cidade diretamente
        console.log(cidade) // 'São Paulo'
        setUsuario({ nome, email })
      })
  }, [])
  
  return <div>{/* ... */}</div>
}
```

---

# Operador Spread
`...`

> "Espalha" elementos de arrays/objetos ou cria cópias

```js {all|3-6|all}
const [form, setForm] = useState({ nome: '', email: '', idade: '' })

// Atualizando apenas um campo
const handleChange = (campo, valor) => {
  setForm({
    ...form,        // Mantém todos os campos existentes
    [campo]: valor  // Sobrescreve apenas o campo específico
  })
}
```

---

# Combinando Objetos com Spread

```js
// Combinando configurações
const defaults = { theme: 'light', lang: 'pt-BR' }
const userConfig = { theme: 'dark', notifications: true }

const config = { 
  ...defaults,    // { theme: 'light', lang: 'pt-BR' }
  ...userConfig   // Sobrescreve theme, adiciona notifications
}
// Resultado: { theme: 'dark', lang: 'pt-BR', notifications: true }

// Passando props com spread
const usuario = {
  nome: 'Ana',
  email: 'ana@email.com',
  idade: 25
}

// Passa todas as propriedades como props individuais
<Usuario {...usuario} />
```

---

# Spread com Arrays

```js
const ListaTarefas = () => {
  const [tarefas, setTarefas] = useState(['Estudar', 'Codar'])
  
  const adicionarTarefa = (novaTarefa) => {
    // Adiciona no final
    setTarefas([...tarefas, novaTarefa])
    
    // Ou adiciona no início
    setTarefas([novaTarefa, ...tarefas])
  }
  
  const removerTarefa = (index) => {
    // Remove item específico
    setTarefas([
      ...tarefas.slice(0, index),
      ...tarefas.slice(index + 1)
    ])
  }
  
  return (/* ... */)
}
```

---

# Ternary Operator (Operador Ternário)

> Substituto do `if/else` em JSX e lógica simples

```js
condicao ? valorSeVerdadeiro : valorSeFalso
```
---

# Ternary Operator
Exemplo (renderização condicional)

```js
const Saudacao = ({ usuario }) => (
  <div>
    {usuario ? (
      <h1>Bem-vindo de volta, {usuario.nome}!</h1>
    ) : (
      <button>Fazer login</button>
    )}
  </div>
)
```

---

# Ternary Operator
Exemplo com React

```js {all|1-6|8-12|14-18|all}
// Classes condicionais
const BotaoEstado = ({ ativo }) => (
  <button className={`botao ${ativo ? 'ativo' : 'inativo'}`}>
    {ativo ? 'Ativo' : 'Inativo'}
  </button>
)
// Renderização condicional de componentes
<>
  {isLoading ? (
    <Spinner />
  ) : (
    <Conteudo dados={dados} />
  )}
</>
// Lista vazia
const Lista = ({ itens }) => (
  <div>
    {itens.length > 0 
      ? itens.map(item => <Item key={item.id} {...item} />)
      : <p>Nenhum item encontrado</p>
    }
  </div>
)
```

---

# ES6 Modules

> Sistema de módulos nativo do JavaScript

```js {all|2-5|7-9|all}
// utils/formatadores.js

// Export nomeado (múltiplos por arquivo)
export const formatarMoeda = (valor) => {
  return `R$ ${valor.toFixed(2)}`
}

// Export default (apenas um por arquivo)
export default {
  moeda: formatarMoeda,
  data: formatarData
}
```

---

# ES6 Modules
`import`

```js {all|2|4|6|8|all}
// Componente.jsx
// Import nomeado (com chaves)
import { formatarMoeda, formatarData } from './utils/formatadores'
// Import default (sem chaves)
import formatadores from './utils/formatadores'
// Renomeando imports
import { formatarMoeda as moeda } from './utils/formatadores'
// Importando tudo
import * as Formatadores from './utils/formatadores'
```

---

# ES6 Modules
Exemplo com React

```js
// components/Botao.jsx
export const Botao = ({ children, onClick }) => (
  <button onClick={onClick}>{children}</button>
)

// components/index.js - Barrel file
export { Botao } from './Botao'
export { Card } from './Card'
export { Input } from './Input'

// App.jsx - importando múltiplos componentes
import { Botao, Card, Input } from './components'
```

---
layout: quote
---

# Promises

> ES6 define uma `Promise` como sendo um objeto que encapsula o resultado de uma operação assíncrona.

---
layout: image-right
image: https://www.javascripttutorial.net/wp-content/uploads/2022/02/JavaScript-Promises.svg
backgroundSize: contain
---

# Promises
Estados

Um objeto `promise` pode assumir os estados:
- *Pending*
- *Fulfilled* junto com um valor
- *Rejected* junto com um motivo

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
Realizar o Quiz ES6 disponível na Aula 4 do Google Classroom.

---

# Referências

- [ES6 Tutorial](https://www.javascripttutorial.net/es6/) 
- [React](https://react.dev/)

---
src: /snippets/end.md
---