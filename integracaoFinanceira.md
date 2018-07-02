## Boleto
  - Registro é obrigatório
  - Campos 
    - Beneficiário: Recebedor
    - Pagador
    - Nosso Número: Número do Banco. Ora o próprio banco gera, ora o cliente gera
    - Número do documento: Código de controle interno do cliente
    - Linha digitável: Representação numérica do boleto
    - Código de Barras: Representação em imagen do boleto
    - É possível gerar o Código de barras através da linha digitável e vice-versa
    - Campo Livre: O Código de Barras é uma string contendo várias informações sobre o boleto. Dentro dessa string há um espaço
    fixo que possui o mesmo tamanho para todos os bancos. Dessa forma, é possível somente implementar a linha digitável de cada 
    banco caso já haja outros bancos implementados
    
    
  - Alguns bancos fornecem Web Services
  - Boleto vencido pode ser pago
  - Juros é opcional
  - Nosso Número
    - Alguns WS criam o nosso número
    - Outros permitem enviar o nosso número
    - Outros permirtem Ambos os casos
    
# VAN
  Os bancos não possuem apis para movimentação de contas de forma automatizada. Para isso existem as VANS.
  
  Grandes empresas utilizam VANS para automatizar seus processos bancários: Pagamento de contas, retornar extrato, 
  retornar arquivo de retorno, enviar arquivos de remessa, transferências ....
  
  VAN é a sigla de Value Added Network, ou Rede de Valor agregado. Trata-se de uma central de comunicação que recebe 
  pedidos de compras e os distribui para as organizações em tempo e formato apropriados. 
  Ela pode fornecer outros serviços similares e é também conhecida como uma rede terceirizada. 
  A Van no Brasil é muito usada por varejistas e grandes empresas de serviços que usam essas “Vans” para receberem dos bancos,
  adquirentes, gateways e sistemas de processamento, arquivos com dados de pagamento e cobrança. 
  Ela faz justamente o intercâmbio com agentes financeiros.

  Por exemplo, em um sistema de intercâmbio eletrônico de dados, uma VAN traduz os códigos utilizados pelo comprador para 
  aqueles usados pelo vendedor e vice-versa. Então, ambas empresas podem ser interligadas sem ter que investir
  na codificação de sistemas de catalogação.
  
  https://blog.vindi.com.br/o-que-e-uma-van/
  
  
  # Cartão de Crédito
    - Pagamento via api
    - A api devolve um código de transação que deve ser guardado, é possível enviar um código de controle/vinculação também.
    
    - Ciclo básico: 
      - Autorização
      - Captura: Confirmação da compra
      - Cancelar
      
