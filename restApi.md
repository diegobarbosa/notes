- Formatos de Endereço:
  - https://api.mysite.com/v1/
  - https://www.mysite.com/api/v1/
  
  
- Versionar pela URL é a boa prática. Através de custom http headers podem ocorrer problemas.
  - https://api.mysite.com/v1/
  
- Usar os verbos HTTP e não nomes indicando ações:
  - Errado:
    - https://api.mysite.com/v1/cadastrarCliente
    - https://api.mysite.com/v1/alterarEnderecoDoCliente
  
  - Certo:
    - POST https://api.mysite.com/v1/cliente //no corpo enviar dados em JSON
    - PUT https://api.mysite.com/v1/cliente/1000/endereco //no corpo enviar dados em JSON
    
    
- Autenticação

  É feita com HttpBasic. Deve-se enviar um Header http no seguinte formato:  **Authorization: Basic ZnJlZDpmcmVk** .
  Onde, **ZnJlZDpmcmVk** é um hash base64 no formato **usuario:senha**


- Paginação

  Usar parâmetros query para paginação:
  
   curl -X GET https://api.mysite.com/v1/clientes/10/telefones/?page=2&per_page=5 \
      -u 'YOUR_API_KEY:' 
     

Parâmetro | Descrição
------------ | -------------
**page:** default 1 | Implementação de uma paginação de resultados do objeto
**per_page:** Default:50 | Retorna n objetos por página



  Referência: https://docs.api.fastnotas.com/#pagina-o



- WebHooks

  São eventos que acontecem dentro da api que notificam via POST uma URL pré determinada pelo cliente.
  Podem ser implementadas através de um componente de QUEUE, RabbitMQ, onde um evento é agendado/colocado na fila 
  para ser enviado/notificado na URL que o cliente informou.
  
  Uma notificação tem sucesso quando o cliente retorna o código HTTP 200. Outro código indica erro e a API
  deve ficar tentando comunicar o evento de tempos em tempos aumentando o espaço entre as requisições.
  O próprio RabbitMQ possui mecanismo de Retry.

  
- Ferramentas de Documentação de API
    - https://swagger.io/
    - https://github.com/lord/slate
    
    
- Exemplos de APIs
  - https://documentation.mailgun.com/en/latest/api_reference.html
  - https://docs.api.fastnotas.com/
  - https://api.nfe.io/sandbox/index
  - https://stripe.com/docs/api
  - https://bestbuyapis.github.io/api-documentation/
  - https://developers.cimediacloud.com/
  
    
    
  
