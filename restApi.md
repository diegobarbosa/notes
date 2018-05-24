# Formatos de Endereço:
  - https://api.mysite.com/v1/
  - https://www.mysite.com/api/v1/
  
# Versionamento
Versionar pela URL é a boa prática. Através de custom http headers podem ocorrer problemas.
  - https://api.mysite.com/v1/
  
# Verbos HTTP
 Usar os verbos HTTP e não nomes indicando ações:
  - Errado:
    - https://api.mysite.com/v1/cadastrarCliente
    - https://api.mysite.com/v1/alterarEnderecoDoCliente
  
  - Certo:
    - POST https://api.mysite.com/v1/clientes //no corpo enviar dados em JSON
    - PUT https://api.mysite.com/v1/clientes/1000/enderecos/10 //no corpo enviar dados em JSON
    
# Plural
Utilize o nome dos recursos no plural.
  - Errado
    - https://api.mysite.com/v1/cliente
    - https://api.mysite.com/v1/cliente/10/fatura
    
  - Certo
    - https://api.mysite.com/v1/clientes
    - https://api.mysite.com/v1/clientes/10/faturas
    
    
# Endpoints da API

Método  |	Endpoint |	Descrição
--------|--------| ---------------
GET |	/company 	| Retorna dados da empresa
GET |	/companies |	Retorna dados das empresas afiliadas à empresa parceira
GET |	/companies/:id |	Retorna uma empresa específica
POST |	/companies |	Cria uma empresa
DELETE |	/companies/:id |	Inativa uma empresa
PUT |	/companies/:id |	Atualiza os parâmetros de uma empresa
GET |	/customers |	Retorna todos clientes
POST |	/customers 	| Cria um cliente
GET |	/customers/:id |	Retorna um cliente
GET | /companies/{company_id}/serviceinvoices | Listar as Notas Fiscais de Serviço (NFSE)
POST |  /companies/{company_id}/serviceinvoices | Emitir uma Nota Fiscal de Serviço (NFSE)
DELETE |  /companies/{company_id}/serviceinvoices/{id} | Cancelar uma Nota Fiscal de Serviços (NFSE)
GET  | /companies/{company_id}/serviceinvoices/{id} | Obter os detalhes de uma Nota Fiscal de Serviço (NFSE)
PUT  | /companies/{company_id}/serviceinvoices/{id}/sendemail | Enviar email para o Tomador com a Nota Fiscal de Serviço (NFSE)
GET  | /companies/{company_id}/serviceinvoices/{id}/pdf | Download do PDF da Nota Fiscal de Serviço (NFSE)
GET  | /companies/{company_id}/serviceinvoices/{id}/xml | Download do XML da Nota Fiscal de Serviço (NFSE
   
# Content-Type

Informar o content-type **Content-Type: application/json**
    
# Autenticação

  É feita com HttpBasic. Deve-se enviar um Header http no seguinte formato:  **Authorization: Basic ZnJlZDpmcmVk** .
  Onde, **ZnJlZDpmcmVk** é um hash base64 no formato **usuario:senha**


# Paginação

  Usar parâmetros query para paginação:
  
   curl -X GET https://api.mysite.com/v1/clientes/10/telefones/?page=2&per_page=5 \
      -u 'YOUR_API_KEY:' 
     

Parâmetro | Descrição
------------ | -------------
**page:** default 1 | Implementação de uma paginação de resultados do objeto
**per_page:** Default:50 | Retorna n objetos por página

Todas as requisições de listagem retornam os dados referentes à paginação através dos seguintes headers http:

HTTP Header| 	Descrição
-----------| -----------
Current-Page| 	Página atual
Total-Pages | Total de páginas
Per-Page 	|Objetos por página

  Referência: https://docs.api.fastnotas.com/#pagina-o



# WebHooks

  São eventos que acontecem dentro da api que notificam via POST uma URL pré determinada pelo cliente.
  Podem ser implementadas através de um componente de QUEUE, RabbitMQ, onde um evento é agendado/colocado na fila 
  para ser enviado/notificado na URL que o cliente informou.
  
  Uma notificação tem sucesso quando o cliente retorna o código HTTP 200. Outro código indica erro e a API
  deve ficar tentando comunicar o evento de tempos em tempos aumentando o espaço entre as requisições.
  O próprio RabbitMQ possui mecanismo de Retry.
  
  Durante a implementação da API poderão existir momentos em que você precisará aguardar alguma ação externa antes de prosseguir com seu   processo. Suponha que você necessite confirmar a emissão de uma nota fiscal antes de emitir a cobrança. Uma prática desaconselhável     seria, por exemplo, agendar uma consulta diária ao serviço de documentos do Fast Notas para verificar o status de emissao de todas as suas notas fiscais pendentes.

  Além de desperdiçar recursos de processamento, você também sofreria com o atraso entre o momento real da emissão e da consulta do webservice. Isso poderia ser resolvido diminuindo o intervalo entre as consultas, porém dependendo do número de notas fiscais pendentes, este método tornaria-se inviável em pouco tempo.

  Para resolver esse problema, inverte-se a responsabilidade da notificação: O Fast Notas avisará você quando alguma ação ocorrer. Este aviso é realizado através de um HTTP POST que o Fast Notas faz em uma URL que você pode configurar na plataforma. Estes avisos são chamados de webhooks.
  
  
## Tipos de Eventos
Evento |	type |	data
------| --------| --------
Documento em processamento |	document_processing |	document
Documento aguardando retorno externo |	document_waiting |	document
Documento emitido/arquivado com sucesso |	document_success |	document
Documento cancelado| 	document_canceled 	|document
Documento com erro |	document_error |	document
Documento rejeitado na emissão/arquivamento |	document_rejected |	document
Operação em processamento |	operation_processing 	|operation
Operação aguardando retorno externo 	|operation_waiting |	operation
Operação efetuada com sucesso |	operation_success |	operation
Operação com erro 	|operation_error|	operation
Operação rejeitada |	operation_rejected |	operation
Arquivo disponível | 	asset_avaliable 	| asset  
  
## Formato e método de envio
  
Todas as requisições geradas a partir de webhooks são efetuadas com o método POST, com o conteúdo no corpo (body) da requisição no formato JSON, incluindo os seguintes headers:

HTTP Header | 	Descrição
------------| ---------------
Content-Type |	application/json; charset=UTF-8
User-Agent | 	mysSiteHookshot/1.0

  A plataforma espera que sua aplicação responda com o código HTTP 2XX (200, 201, etc) em no máximo 20 segundos. Códigos de redirecionamento (3XX) não serão seguidos e serão considerados como falha.


## Retentativas

A plataforma Fast Notas irá efetuar 15 retentativas de envio caso seu sistema esteja fora do ar ou responda com um código HTTP diferente de 2xx. As retentativas são enviadas em intervalos progressivos durante aproximadamente 48 horas. Depois desse período a notificação é descartada.

## Conteúdo da requisição

Como mencionado acima, o conteúdo da requisição estará contido em seu no corpo (body), no formato JSON.
O conteúdo do atributo data irá depender do tipo de evento enviado e respeitará o mesmo formato da API REST.

      {
      "event": {
        "type": "document_processing",
        "created_at": "2017-01-19T00:58:20.835Z",
        "data": {
          "document": {
            ...
          }
        }
      }
    }


## Boas práticas

Em condições normais de operação dificilmente esse limite será atingido, porém más práticas de integração podem comprometer o limite rapidamente.

### Evite polling

Polling é o nome do procedimento usado para buscar o status de determinada informação em intervalos de tempo consecutivos. Sabemos que é comum implementar rotinas diárias de consulta de status. Enquanto este procedimento funciona satisfatoriamente com um número baixo de registros, você poderá ultrapassar o limite de requisições caso o número de consultas aumente.

É justamente por isso que a plataforma Fast Notas oferece os webhooks. Em vez de gastar recursos computacionais com polling, configure a plataforma Fast Notas para avisar seu backend via POST imediatamente quando um evento ocorrer. Com isso você não desperdiça recursos e garante que sua plataforma estará com os dados sempre atualizados. Se você precisar de um tipo de webhook que ainda não esteja disponível, converse com nossa equipe e ficaremos felizes em criar um novo tipo de disparo que ajude você a se manter dentro do limite de requisições.

### Use cache

Recursos que não são atualizados frequentemente podem ser armazenados em cache localmente. Por exemplo, em vez de efetuar uma requisição de listagem de documentos toda vez que um cliente quiser visualizar o status da sua nota fiscal, faça uma única consulta à API e armazene o resultado, configurando o tempo de expiração que julgar necessário. Soluções baseadas em memcache ou Redis funcionam muito bem nesses casos.


# HTTP status codes

A API segue o padrão que usa códigos de resposta HTTP convencionais para indicar o sucesso ou fracasso de uma solicitação da API. Em geral, os códigos na gama 2xx indicam sucesso, os códigos na gama 4xx indicam um erro dada a informação fornecida (por exemplo, um parâmetro necessário foi omitido, ou informado com um valor errado, etc) e os códigos na gama indicam um 5xx de erro com os servidores da lista (esses são raros).



Código |	Significado
-------|-------------
200 - OK |	Request realizado com sucesso
201 - Created |	Cadastro criado com sucesso
204 - No Content |	Requisição sem conteúdo
400 - Bad Request |	Erro de sintaxe JSON no corpo do request
404 - Not Found |	Registro não encontrado
422 - Unprocessable Entity |	Parâmetros inválidos. Verificar erro na resposta
429 - Too Many Requests |	Limite de requisições excedido
500 - Internal Server Error |	Erro interno do servidor


  
# Ferramentas de Documentação de API
   - https://swagger.io/
   - https://github.com/lord/slate
    
    
# Exemplos de APIs
  - https://documentation.mailgun.com/en/latest/api_reference.html
  - https://docs.api.fastnotas.com/
  - https://api.nfe.io/sandbox/index
  - https://stripe.com/docs/api
  - https://bestbuyapis.github.io/api-documentation/
  - https://developers.cimediacloud.com/
  
    
    
  
