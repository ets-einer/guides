---
theme: seriph
---

# Programação assíncrona e paralelismo
Possibilitando resolver problemas mais rápidos de forma multitarefa.

A programação assíncrona nos permite parar e retomar a execução de determinados blocos de código conforme o necessário.
Este aspecto da programação é mandatório em qualquer linguagem utilizada hoje em dia, pois permite que uma operação que está
esperando algo para continuar (como por exemplo uma requisição feita via internet) não bloqueie as outras. 

Em um sistema síncrono, quando o código interage com elementos do mundo de fora, como por exemplo ler um arquivo,
absolutamente tudo deve parar e esperar, até que a operação de leitura do arquivo termine, assim permitindo com que o resto do programa
rode.

Em um sistema assíncrono operações que não dependem uma da outra podem rodar em paralelo, extraindo o máximo de performance possível.

Um exemplo interessante disto no javascript seria:
Enquanto uma requisição é feita via internet, a página inteira perde a funcionalidade. Não é possível clicar em um botão sequer, e as
animações param de reagir. Isto é o que acontece quando o javascript é executado de maneira totalmente síncrona.

---

 ## Promises

Uma promise, basicamente, simboliza um valor que não necessariamente é conhecido quando a promise é criada.
Pense nisso como literalmente uma promessa de que no futuro um valor irá vir para esta variável.

Um claro exemplo disso é imaginar um microondas que pode esquentar a comida ou se explodir:

```ts
function inserirNoMicroondas(objeto: string, tempo: number) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            if (objeto == 'talher') {
                reject('Microondas explodiu')
            } else {
                resolve(objeto + ' quente')
            }
        }, tempo)
    })
}
```

---

E agora podemos utilizar a nossa função.

```ts
inserirNoMicroondas('banana', 15000)
    .then(valor => {
        console.log(valor); // 'banana quente' após 15 segundos
    })
    .catch(err => {
        console.error(err); // Não cairá no erro
    });

inserirNoMicroondas('talher', 10000)
    .then(valor => {
        console.log(valor) // Esta promise não irá dar certo
    })
    .catch(err => {
        console.error(err); // 'Microondas explodiu'!
    })
```

---

## Promises no JavaScript moderno

Podemos utilizar a sintaxe `async` e `await`:

```ts
async function cozinharAlmoco() {
    const resultado = await inserirNoMicroondas('melancia', 2500);
    // Execução deste bloco de código para aqui até a promise ser concluída
    
    console.log(resultado); // -> 'melancia quente'
}

// await + sintaxe com callbacks -> favor, não utilizar
await inserirNoMicroondas('melancia', 2500)
    .then(resultado => {
        console.log(resultado)
    })
```
---

Promises com a sintaxe await tem um código melhor, até precisarmos fazer *error handling*...

```ts
async function cozinharAlmoco() {
    const resultado = await inserirNoMicroondas('talher', 5000); // Esse código vai explodir

    // Não podemos usar o .catch para tratar o caso de erro
    console.log(resultado);
}
```

Mas podemos utilizar o bloco `try` e `catch`:

```ts

async function cozinharAlmoco() {
    try {
        const resultado = await inserirNoMicroondas('talher', 5000);
        console.log(resultado);
    } catch (err) {
        console.error(err); // O código vai vir para cá, quando o erro estourar
    }
}
```

---

Também é possível fazer assim, caso não queira fazer mil `try` `catch` um dentro do outro.

```ts
import { handleMyError } from './helpers';

async function cozinharAlmoco() {
    let resultado;
    try { resultado = await inserirNoMicroondas('talher', 5000); } 
    catch (err) { handleMyError(err); }

    console.log(resultado);
}
```

---

Usamos a sintaxe *await* para quando esperamos o resultado de uma operação assíncrona para podermos utilizar outra função assíncrona, no entanto, caso não precisamos utilizar o resultado de uma *Promise* em outra chamada de função assíncrona, podemos executá-las de forma concorrente e independentes.

Nós usamos a função `Promise.all()` passando como parâmatro um array de *Promises* para executar múltiplas *Promises* independentemente:

```ts
async function fetchAllData() {
    const [posts, noticias, topicos] = await Promise.all([
        fetch('/api/posts'),
        fetch('/api/noticias'),
        fetch('/api/topicos')
    ]);

    return { posts, noticias, topicos };
}

const allResponses = await fetchAllData() // só vai retornar esse dado quando todas as 3 promises serem resolvidas
```
