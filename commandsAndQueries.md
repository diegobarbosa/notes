## Commands

A seguir estão diversos patterns que tenho usado em meu dia-a-dia.


## CQRS / CQS / Commands and Queryes
Toda aplicação, seja web, seja command line, seja desktop, seja mobile consiste basicamente de: informar um input ao programa, o programa interpreta e executa o comando, esse comando, executa uma operação em memória (algum calculo)  ou interage com I/O (lê ou escreve de alguma fonte de dados: FileSystem, Banco de dados, Queue, ApiWeb...)

[http://cdn.guru99.com/images/stories/blackbox.png]

Basicamente existem dois tipos de comando para ser executados por um computador: Execute [uma operação / e grave um dado em uma fonte de dados] e Leia de uma fonte de dados. Read Command e Query.

Logo, precisamos interpretar toda entrada como sendo write/read, command/query. Em um ambiente web cada link e post (submissão de formulário) é um comando enviado ao servidor. Esses comandos vão ser ligados a actions por meio de urls e dos verbos HTTP. Cada action em um controller web é um comando ou query que o usuário/sistema externo espera que execute uma ação ou retorne algum valor.

Em um programa de linha de comando, cada sub-comando (que progravelmente seria tratado com um switch-case ou if-else) é um command/query. Em um aplicativo desktop/mobile cada evento é um command/query.

**Add código Exemplo de controller, desktop e comand line

Poderiamos escrever nossos programas diretamente dentro dessas actions/eventos/switch-cases que nosso programa funcionaria. Porém, é uma boa prática adicionar uma camada de abstração que fizesse nosso programa ficar independente de framework e ambiente.

Para isso podemos lançar mão dos Patterns Command e Mediator.

O Command
