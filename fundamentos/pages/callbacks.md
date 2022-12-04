---
theme: seriph
---

# Callbacks

Trate funções como qualquer outro valor.

```ts
function hello() {
    // ...
}

console.log(typeof hello) // -> 'function' 
// hello é uma variável do tipo função!
```

Com isto em mente, também é possível definir funções sem utilizar a keyword **function**,
utilizando a sintaxe das *arrow functions*.

```ts
const name = 'Viktor'; // -> String 
const hello = () => { // -> Function
    // ... 
};
```

---

Indo um pouco mais além, como uma função é como qualquer outro valor, podemos receber funções via parâmetros, em outras funções.

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
criando assim o que chamamos função anônima.

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