---
theme: seriph
---

# Var, let e const
As três maneiras de criar uma variável

```js {all|1-4|5-13|14-16|16-18|19-21|all}
var wilson = 'bom dia';
var wilson = 'sinistro'; // não gera problemas

console.log(wilson); // -> 'sinistro'

// PONTO PROBLEMATICO DO VAR

if (true) {
    var wilson = 'tongo';
}

console.log(wilson); // -> 'tongo' mesmo que esteja fora do escopo

let dispositivo = 'telefone';
let dispositivo = 'impressora'; // Gera um erro

let pessoa = 'prates';
pessoa = 'gabirel'; // 👍 tudo ok

const bicho = 'peixe';
bicho = 'camelo'; // Gera um erro


```