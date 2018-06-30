# Requisições Json

## content-type: application/x-www-form-urlencoded;

 Aceita o Body com Json 
        
        [HttpPost]
        [Route("api/pessoa")]
        public object SalvarNovoAtendimento( Pessoa pessoa)
        {
            return Json(new pessoa);
        }
        
## content-type: application/json;

Precisa colocar [FromBody] se não os parametros não são preenchidos.

        [HttpPost]
        [Route("api/pessoa")]
        public object SalvarNovoAtendimento([FromBody]  Pessoa pessoa)
        {
             if(!ModelStatus.IsValid)
                  return BadRequest(ModelState); // retorna {"pacienteDataNascimento":["The input was not valid."]}
        
            return Json(new pessoa);
        }
        
Caso haja algum parâmetro/propriedade inválido, do tipo:
  - um campo int que foi passado uma string, ex: {idPessoa:"uma string"}
  - um campo DateTime que foi passado uma string inválida, ex: {dataNascimento:"hoje"}

O model/parâmetro **pessoa** será null pois o fluxo é interrompido na validação, dentro do framework.

Nesse caso, é necessário fazer vide o exemplo acima. Tem que checar se ModelStatus.IsValid.
      
     
    
        
