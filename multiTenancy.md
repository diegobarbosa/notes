## Master-Slave
	- Single Master (one only Write) ==> Multiple Slaves (only Read)
	- Multi Master (multiple Write) ==> Multiple Slaves (only Read)
	
## Types of Partitioning
	- Divide a Table
		- Horizontal Partitioning
		- Vertical Partitioning
	- Divide a data set / schema
		 - Functional Partitioning: Store Front, Search, Carrinho de Compras
		 

## Shard
A database shard is a horizontal partition of data in a database or search engine. 
Each individual partition is referred to as a shard or database shard. 
Each shard is held on a separate database server instance, to spread load.
Acho que no geral, sharding por hash key não é uma boa opção. Como ficam os joins, os backups, a manutenção dos BDs....?

-Tipos
	- Hash Key:
		- Localização: Cidade, Estado, País
		- Sharding by customer or tenant
		- Sharding a graph
		- Sharding Time
	- Funcionality
		- Store Front, Search, Carrinho de Compras


## MultiTenant
Vários clientes usando um mesmo serviço: SASS 

  - Exemplos
    - Shopfy
    - Vtex
    - Uol Ecommerce
    - Vários outros
    
	- Imprescindível ter um tenant_id. Esse será uma coluna para cada tabela
  - SaaS applications

	- Cenários:
		- Um único banco com todos os tenats 
			- Um cliente pode consumir mais recursos que outros. 
			- Dificuldade para escalar
			- Mais fácil de começar
			- Em determinados nichos pode funcionar durante anos assim
			- Pode começar com uma única máquina
		- Um único banco com um squema por tenant
			- Um cliente pode consumir mais recursos que outros. 
			- Com balancear? 
			- Com fazer sharding?
			- Dificuldade para escalar
			- Pode começar com uma única máquina
		- Um BD monolito para cada tenant (cliente): 
			- Cada tenant pode usar uma estratégia diferente de escalabilidade:
				- Sharding
				- Master-Slave
				- Facilidade para escalar
				- Pode começar com uma única máquina
		- Microservices: Divisão pode funcionalidade
      			- Load Balance: Com suporte a script. Permite criar regras mais robustas e complexas, modificar a requisição e passar para 
a app correta.
			- Mais escalável
			- Cada funcionalidade (frente de loja, busca de produto, carrinho, checkout...) possui seu próprio sistema/microservice
			- Dentro de cada microsevice podemos ter uma estratégia diferente de armazenamento de dados:
				- Cada tabela ter o seu próprio tenant_id
				- Um BD para cada cliente
				- Sharding/Master-Slave para determinados clientes
				- Possibilidade de escalar cada cliente individualmente
        
- Referências
  - https://www.citusdata.com/blog/2017/08/28/five-data-models-for-sharding/
  - https://www.slideshare.net/squadette/evan-ellis-tumblr-massively-sharded-mysql
  
