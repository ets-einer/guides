# Operador Spread
Trabalhe com grandes estruturas de dados com poucas linhas de código.

Para conseguirmos entender o operador spread, precisamos aprender o que são os iteráveis.

Um iterável é um objeto que pode ser iterado utilizando a sintaxe `for...of`, alguns exemplos são arrays, objetos e strings.

```ts {all|1-3|5-7|9-|9|10|12,14|13|15-}
for (const x of "oraci") {
  console.log(x) //o,r,a,c,i
}

for (const x of [1,3,6,9]) {
  console.log(x) //1,3,6,9
}

const pessoa = { name: "Pirulete", age: 23 + 1 }
let propriedade: keyof typeof pessoa;

for (propriedade in pessoa) {
  console.log(`${propriedade}: ${pessoa[propriedade]}`);
}
// name: Pirulete
// age: 24
```

---

## Operador Spread (...)

O operador spread é uma sintaxe que possibilita um iterável para ser expandido em lugares onde zero ou mais argumentos (chamadas de função) ou elementos (for array literals) são esperados.

Em um object literal, o operador spread enumera as propriedades de um objeto e os adiciona no objeto a ser criado.

```ts {all|1|3|5,6|8-9|11-12|14|15|16}
const numbers: [number, number, number] = [1, 2, 3];

function sum(x: number, y: number, z: number) { return x + y + z; }

console.log(sum(...numbers)); // 6
console.log(sum.apply(null, numbers)); // 6

const array = [1, 2, 3];
const obj = { ...array }; // { 0: 1, 1: 2, 2: 3 }

const obj1 = { foo: 'bar', x: 42 };
const obj2 = { foo: 'baz', y: 13 };

const clonedObj = { ...obj1 }; // { foo: "bar", x: 42 }
const mergedObj = { ...obj1, ...obj2 }; // { foo: "baz", x: 42, y: 13 }
const updatedObj = { ...obj1, x: 24 } // { foo: "bar", x: 24 }

```


