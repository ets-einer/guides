---
theme: seriph
---

# Escopo das variáveis

```js {all|3-16|9-13}
let wilson = 'ola'; // Variável no escopo global

function miar() {
    let mensagem = 'miaw'; // Variável no escopo da função

    console.log(mensagem) // -> Aqui tudo ok
    console.log(wilson) // -> Aqui também

    if (mensagem == 'miaw') {
        let animal = 'gato'; // Variável no escopo do bloco if

        console.log(animal); // -> Chuchu beleza
    }

    console.log(animal) // -> Esta linha gera um erro (ReferenceError: animal is not defined)
}

console.log(mensagem) // -> Aqui dá erro (ReferenceError: mensagem is not defined)
```