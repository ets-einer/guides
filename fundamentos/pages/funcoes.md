---
theme: seriph
---

# Funções

Trate funções como qualquer outro valor (funções como cidadões de primeira classe)

Uma função nada mais é do que uma variável que contém um código que será executado, ela pode receber parâmetros e retorna um valor, no contexto de programação funcional, uma função recebe um valor o transforma e retorna o novo valor transformado.

```ts
function hello() {
    // ...
}

console.log(typeof hello) // -> 'function' 
// hello é uma variável do tipo função!
```

Com isto em mente, também é possível definir funções sem utilizar a keyword **function**,
utilizando a sintaxe das *arrow functions* (ou funções anônimas) e atribuindo elas à uma variável.

```ts
const name = 'Viktor'; // -> String 
const hello = () => { // -> Function
    // ... 
};
```

---

Indo um pouco mais além, como uma função é como qualquer outro valor, podemos receber funções via parâmetros, em outras funções (também chamado de funções de alta ordem).

```ts
function executarFuncao(fun: Function) {
    fun();
}

const sayHello = () => {
    console.log('hello')
}

executarFuncao(sayHello); // -> 'hello'!
```

Também podemos declarar as funções diretamente ao passarmos argumentos para uma função, utilizando a sintaxe de *arrow function*,
criando assim o que chamamos função anônima (não colocamos nome nela).

```ts
function executarFuncao(fun: Function) {
    fun();
}

executarFuncao(() => {
    console.log('wilson')
}) // -> 'wilson'!
```

---

Sabendo disto, eu poderia por exemplo, criar uma função chamada **useEffect**, e dizer que ela recebe dois argumentos, uma função e um array.

```ts
function useEffect(funcao: Function, deps: Array<any>) {
    // ...
}

// Na hora de chamar ela, ficaria mais ou menos assim:

useEffect(() => {
    // ...
}, [])
```

Essa forma de passar funções como parâmetro de uma outra função e essa outra função chamar a função que foi passada como parâmetro é chamada de **Callbacks**.

```ts
interface Usuario { name: string, age: number }

const pegarUsuario = async (callback: (usuario: Usuario) => any) => {
    const usuario: Usuario = await fetch('/auth/users/me');
    callback(usuario)
}

pegarUsuario((usuario) => { console.log("Eu sou:", usuario) })
```

---

## Closures

É a combinação de duas ou mais funções juntas, onde a função interna tem acesso as variáveis da função externa (fora do seu escopo local).

```ts
function inicializar() {
  var nome = 'Verdura'; // nome é uma variável local criado por inicializar.
  function printarNome() { // printarNome() é a função interna, um closure.
    console.log(nome); // uso da variável declarada pela função parente
  }
  printarNome(); // Chamada da closure dentro da função parente inicializar
}
inicializar(); // Verdura

```
Também podemos retornar a closure da função parente:

```ts
function fazerFuncao() {
  const nome = 'Julia';
  function printarNome() { console.log(nome); }
  return printarNome;
}

const minhaFuncao = fazerFuncao();
minhaFuncao(); // Julia

```

---

## IIFE (Immediately invoked function expression)

IIFE é um recurso da linguagem JavaScript que possibilita chamar uma função assim que declarada:

```ts
(() => {
  // some initiation code
  let firstVariable;
  let secondVariable;
})();
```

Também podemos executar funções assíncronas logo após elas serem declaradas:

```ts
const getFileStream = async (url) => {
  // implementation
};

(async () => {
  const stream = await getFileStream("https://domain.name/path/file.ext");
  for await (const chunk of stream) {
    console.log({ chunk });
  }
})();

```

---

## Currying

Muito utilizado no cálculo lambda, o Currying é uma técnica que possibilita simular uma função com múltiplos parâmatros usando apenas funções que recebem apenas um parâmetro.

```ts
// Sem curry
const adicionar = (a: number, b: number, c: number) => {
    return a+ b + c
}
console.log(adicionar(2, 3, 5)) // 10

// Com curry
const adicionarCurry = (a: number) => {
    return (b: number) => {
        return (c: number) => {
            return a+b+c
        }
    }
}
console.log(adicionarCurry(2)(3)(5)) // 10
```

Essa técnica é muito utilizada para simplificar chamada de funções, ou para abstrair algum comportamento na utilização de funções.

---

## Memoização

É uma técnica de otimização que deixa aplicações mais eficientes, ele faz isso em duas etapas: 
1. Armazena os resultados de uma computação no *cache*
2. Pega os resultados calculados do *cache* caso requisitado

<br>

```ts
// É necessário saber o que são os *closures* e as funções de alta ordem.
interface Memo { [key: number]: number; }

const fib = (n: number): number => {
  if (n <= 1) return 1;
  return fib(n - 1) + fib(n - 2);
};

const fibMemo = (n: number, memo?: Memo): number => {
  memo = memo || {};
  if (memo[n]) return memo[n];
  if (n <= 1) return 1;
  return (memo[n] = fibMemo(n - 1, memo) + fibMemo(n - 2, memo));
};

timeFunction(fib, [20]); // fib took 1.2142000012099743 millisecond
timeFunction(fibMemo, [20]); // fibMemo took 0.06120000034570694 milliseconds
```