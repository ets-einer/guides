---
theme: seriph
---

# Promises

Uma promise, basicamente, simboliza um valor que não necessariamente é conhecido quando a promise é criada.
Pense nisso como literalmente uma promessa de que no futuro um valor irá vir para esta variável.

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

inserirNoMicroondas('banana', 15000)
    .then(valor => {
        console.log(valor); // 'banana quente'
    })
    .catch(err => {
        console.error(err); // Não cairá no erro
    });
```
---


```ts
inserirNoMicroondas('talher', 10000)
    .then(valor => {
        console.log(valor) // Esta promise não irá dar certo
    })
    .catch(err => {
        console.error(err); // 'Microondas explodiu'!
    })
```

# Promises no javascript moderno

Sintaxe async e await

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

    // Não podemos usar o .catch
    console.log(resultado);
}

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

```ts
import { handleMyError } from './helpers';

async function cozinharAlmoco() {
    let resultado;
    try { resultado = await inserirNoMicroondas('talher', 5000); } 
    catch (err) { handleMyError(err); }

    // Também é possível fazer assim, caso não queira fazer mil try catches um dentro do outro.
    console.log(resultado);
}
```

Executando múltiplas promises independentes paralelamente com **Promise.all**

```ts
async function fetchAllData() {
    const [posts, noticias, topicos] = await Promise.all([
        fetch('/api/posts'),
        fetch('/api/noticias'),
        fetch('/api/topicos')
    ]);

    return { posts, noticias, topicos };
}
```