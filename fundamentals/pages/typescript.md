# TypeScript

O que é, o que resolve e como usá-lo

O TypeScript é uma linguagem criada pela Microsoft em 2012 open source que é um superset, ou seja, incluí toda sintaxe do JavaScript mas também possui sua própria sintaxe.

Ele foi criado com o objetivo de resolver dois grandes problemas encontrados no JavaScript, compatibilidade e a falta de um sistema de tipos.

---

## Compatibilidade

O JavaScript é uma linguagem que possuí muitas variações, ele foi criado junto com o navegador Netscape Navigator por Brendan Eich com o objetivo de deixar as páginas mais dinâmicas, mas logo após seu lançamento já havia dezenas de versões melhoradas ou pioradas dessa linguagem.

É com esse problema que foi determinado a especificação padrão do que seria o JavaScript, o EcmaScript, com o objetivo de garantir a interoperabilidade entre as páginas web em diversos navegadores.

Assim surgiu diversas versões lançadas do EcmaScript, que vão desde a ES1 (1997), até a ES 2022 (temos também a ES Next que possuí as próximas features que serão implementadas na linguagem).

No entando, alguns navegadores não possuem suporte para as versões mais recentes do EcmaScript, e o TypeScript resolve este problema pois ele consegue transpilar para qualquer versão do ES.

---

## Sistema de tipos

O EcmaScript define o JavaScript como sendo uma linguagem dinâmica, ou seja, os tipos das variáveis são determinados em runtime (tempo de execução), porém isso pode acarretar em um comportamento não desejado, um exemplo de absurdo é isso:

```js
const wirso = ('b' + 'a' + + 'a' + 'a').toLowerCase()
console.log(wirso) // banana
```

Para evitar essas bizarrices, o TypeScript fornece para nós um sistema de tipos no Compile time(tempo de compilação) que previne fazer operações indesejadas com tipos inadequados.

---

## Como usá-lo?

Na declaracão de toda variável, é possível associar um tipo à ela:

```ts
const balta: string = "sirene"
let idade: number = 19
const inteligencia: null = null
let dataDaApresentacao: undefined = undefined
const isGatoVivo: "vivo" | "morto" = "vivo"
```

Por sorte, quase sempre o compilador consegue *inferir* o tipo automaticamente para você

```ts
let galerinha = 'do mal'; // -> tipo inferido: string

galerinha = 25 // -> Typescript te avisa com um erro: 
// Não é possível colocar um número em uma variável anteriormente definida como string.
```

---

Também é possível adicionar tipo em estruturas de dados básicas como arrays e objetos

```ts
const feio: string[] = ["natha", "oraci"]

interface Produto {
  nome: string;
  precoEmReais: number;
  pesoEmKg: number;
}

let parafusadeiraBosch: Produto {
  nome: "Parafusadeira Bosch Go À Bateria 3,6v Bivolt 110/220v",
  precoEmReais: 459.70,
  pesoEmKg: 0.31
}
```

---

Valores de uma interface ou tipo podem ser opcionais:

```ts
interface Cidade {
  nome: string;
  populacao: number;
  isLimpo?: boolean;
}
```

Funções também podem ser tipadas utilizando o TypeScript:

```ts

type funcaoDeNumero = (numero: number) => number

const dobraNumero: funcaoDeNumero = (numero) => numero * 2
const metadeNumero: funcaoDeNumero = (numero) => numero / 2

const raizQuadrada: funcaoDeNumero = (numero) => {
  for (var i = 0; i * i <= numero; i++) {
    if (i * i === numero)
      return i;
  }
  return numero;
}
```

---

Ou até mesmo objetos com funções:

```ts
type Pessoa = {
  nome: string;
  idade: number;
  posicao: [number, number]
  mover: (posicao: [number, number]) => Pessoa
  envelhecer: () => Pessoa
}
const prates: Pessoa = {
    nome: "Prates",
    idade: 19,
    posicao: [-22.9691, -46.9958], // Valinhos coordenadas
    mover: posicaoNova => { prates.posicao = posicaoNova; return prates },
    envelhecer: () => { prates.idade += 1; return prates }
}
console.log(prates.idade) // 19
console.log(prates.envelhecer())
// {
//   "nome": "Prates",
//   "idade": 20,
//   "posicao": [
//     22.9691,
//     46.9958
//   ]
// }
```

