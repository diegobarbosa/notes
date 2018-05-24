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

Todas as requisições de listagem retornam os dados referentes à paginação através dos seguintes headers http:

HTTP Header| 	Descrição
-----------| -----------
Current-Page| 	Página atual
Total-Pages | Total de páginas
Per-Page 	|Objetos por página

  Referência: https://docs.api.fastnotas.com/#pagina-o



- WebHooks

  São eventos que acontecem dentro da api que notificam via POST uma URL pré determinada pelo cliente.
  Podem ser implementadas através de um componente de QUEUE, RabbitMQ, onde um evento é agendado/colocado na fila 
  para ser enviado/notificado na URL que o cliente informou.
  
  Uma notificação tem sucesso quando o cliente retorna o código HTTP 200. Outro código indica erro e a API
  deve ficar tentando comunicar o evento de tempos em tempos aumentando o espaço entre as requisições.
  O próprio RabbitMQ possui mecanismo de Retry.
  
  Durante a implementação da API poderão existir momentos em que você precisará aguardar alguma ação externa antes de prosseguir com seu   processo. Suponha que você necessite confirmar a emissão de uma nota fiscal antes de emitir a cobrança. Uma prática desaconselhável     seria, por exemplo, agendar uma consulta diária ao serviço de documentos do Fast Notas para verificar o status de emissao de todas as suas notas fiscais pendentes.

  Além de desperdiçar recursos de processamento, você também sofreria com o atraso entre o momento real da emissão e da consulta do webservice. Isso poderia ser resolvido diminuindo o intervalo entre as consultas, porém dependendo do número de notas fiscais pendentes, este método tornaria-se inviável em pouco tempo.

  Para resolver esse problema, inverte-se a responsabilidade da notificação: O Fast Notas avisará você quando alguma ação ocorrer. Este aviso é realizado através de um HTTP POST que o Fast Notas faz em uma URL que você pode configurar na plataforma. Estes avisos são chamados de webhooks.
  
    - Formato e método de envio
  
    Todas as requisições geradas a partir de webhooks são efetuadas com o método POST, com o conteúdo no corpo (body) da requisição no formato JSON, incluindo os seguintes headers:

HTTP Header | 	Descrição
------------| ---------------
Content-Type |	application/json; charset=UTF-8
User-Agent | 	mysSiteHookshot/1.0

  A plataforma espera que sua aplicação responda com o código HTTP 2XX (200, 201, etc) em no máximo 20 segundos. Códigos de redirecionamento (3XX) não serão seguidos e serão considerados como falha.


    - Retentativas

A plataforma Fast Notas irá efetuar 15 retentativas de envio caso seu sistema esteja fora do ar ou responda com um código HTTP diferente de 2xx. As retentativas são enviadas em intervalos progressivos durante aproximadamente 48 horas. Depois desse período a notificação é descartada.

    - Conteúdo da requisição

Como mencionado acima, o conteúdo da requisição estará contido em seu no corpo (body), no formato JSON.
O conteúdo do atributo data irá depender do tipo de evento enviado e respeitará o mesmo formato da API REST.



  
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
  
    
    
  
