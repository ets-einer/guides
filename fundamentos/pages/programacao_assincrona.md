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
