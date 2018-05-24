- Formatos de Endereço:
  - https://api.mysite.com/v1/
  - https://www.mysite.com/api/v1/
  
- Versionar pela URL é a boa prática. Através de custom http headers podem ocorrer problemas.
  - https://api.mysite.com/v1/

  
- Usar os verbos HTTP e não nomes indicando ações:
  - Errado:
  https://api.mysite.com/v1/cadastrarCliente
  https://api.mysite.com/v1/alterarEnderecoDoCliente
  
  - Certo:
  POST https://api.mysite.com/v1/cliente //no corpo enviar dados em JSON
  PUT https://api.mysite.com/v1/cliente/1000/endereco //no corpo enviar dados em JSON
  
  - Ferramentas de Documentação de API
  
