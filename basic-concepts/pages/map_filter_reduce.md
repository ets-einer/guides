# Map, Filter e Reduce

Utilizando o array do JavaScript (que na verdade é um objeto), podemos ter acesso à diversas funções para trabalhar com elas, vindo do mundo da programação funcional, temos as funções `map`, `filter` e `reduce`.

Elas permitem usar funções sobre os items do array, o que muitas vezes elimina a necessidade de usar o statement `for` ou `while`, substituindo o por expressões (código que é avaliado para um valor).

## Map

```ts {all|1-3|5|7|9}
function dobraNumero(numero: number) {
  return numero * 2
}

array = [1,5,2,3,23,92,8]

console.log(array.map(dobraNumero)) // [ 2, 10, 4, 6, 46, 184, 16 ]

console.log(array.map((numero: number) => numero * 2)) // [ 2, 10, 4, 6, 46, 184, 16 ]
```
---

## Filter

```ts {all|1-3|5|7|all}
function ePar(numero: number) {
  return numero % 2 === 0
}

array = [1,5,2,3,23,92,8]

console.log(array.filter(ePar)) // [ 2, 92, 8 ]
```

## Reduce

```ts{all|1-3|5|13|6|7|8|9|10-11}
function somar(primeiro: number, segundo: number) {
  return primeiro + segundo
}

array = [1,5,2,3,23,92,8]
// 1 + [5,2,3,23,92,8]
// 1 + 5 + [2,3,23,92,8]
// 1 + 5 + 2 + [3,23,92,8]
// 1 + 5 + 2 + 3 + [23,92,8]
// ...
// 1 + 5 + 2 + 23 + 92 + 8 = 134

console.log(array.reduce(somar)) // 134
```