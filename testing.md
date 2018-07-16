## Unit Testing
Testa o comportamento de uma classe/método de forma isolada. Testa métodos, construtores e propriedades 
(que também são uma forma de método). 
Métodos vão alterar a estrutura interna do objeto e/ou executar uma operação e retornar um valor.

Cada cenário de teste deve ter um contexto (entradas e saídas) bem específico.
Se uma classe A depende de outra classe B, essa outra classe B deve ser mockada. Pois, os cenários de testes da classe A devem ter
um contexto bem específico, e não deve ficar a revelia de bugs ou inconsistências ou intermitências 
ou não determinismo de outras classes.

## Integration Testing
Testa o comportamento/funcionamento de duas classes/componentes em conjunto. Precisamente, testa o comportamento/método de uma classe A 
usando uma outra classe real B, onde A.funtion(B) { B.execute() } .
B pode ser tanto uma classe que executa uma operação em memória, quanto executa uma operação de I/O 
(Disco, Arquivos, Rede, Banco de dados) .

Outro exemplo de integration testing é quando temos uma API Http e um cliente UI em Angular/Razor/Console/Android e criamos todo
o ambiente para testar um crud por exemplo. Ou quando simulamos o upload de um arquivo em uma página e esse arquivo é processado
e o resultado é possível ser checado em outra página. Dessa forma estamos testando componentes de forma integrada.

Functional Testing/System testing/ End to End Testing são uma forma de Integration testing. Na minha opnião esses três tipos de 
testes são a mesma coisa. Testam se um requisito está funcionando de forma correta. 
Ex: Quando clico nesse botão da tela, seja Angular, Razor ou  Android, para salvar os dados, os dados estão sendo salvos e exibidos na tela de exibição? 
Está aparecendo na tela de busca?
Quando salvo os 

