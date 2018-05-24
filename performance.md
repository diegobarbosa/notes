Tipos de Caching
 - Navegador
 - CDN
 - Servidor web (o próprio servidor, NGINX, nuster, HAProxy, Varnish, Squid)
 - Servidor de aplicação (cache de action, redis, memcache)


- Minificar JS e CSS
- Compactar imagens



- CDN
  - Mesmo no brasil value muito a pena ter um CDN pois o mesmo aumenta a velocidade do acesso às páginas web
  diminuido o tempo de carregamento.
  
  - O que empurrar para o CDN? JS, CSS, Imagens, fontes, banners, páginas inteiras. Resultado de apis? 
  
  - Referências
    - https://blog.umbler.com/br/mitos-e-verdades-sobre-o-uso-de-cdn-parte-1-cache/
    - https://techinbrazil.com.br/7-dicas-para-estabelecer-um-cdn-pop-no-brasil
    - https://techinbrazil.com.br/100-provedores-de-co-locacao-no-brasil
    - https://www.ecommercebrasil.com.br/artigos/12-bons-motivos-para-voce-usar-uma-cdn-parte-1/
  
  - Vantagens:
    - Diminui tempo de carregamento 
    - Melhora a percepção do loading
    - Diminui o uso de recursos no servidor: Menos tráfego, menos requisições, menos arquivos sendo enviados
    - Redução na quantidade de máguinas cloud
    - Redução do uso do tráfego das máquinas, que também é cobrado, que deixam de servir arquivos estáticos
    – o site fica no ar, já que não extrapola os limites de tráfego e hardware impostos pelo provedor de hospedagem, evitando ser penalizado por isso.
    – a fatura no final do mês sofre uma redução brutal, pois há menos consumo de banda e recursos de hardware.
    
  
  - No Brasil:  
    - www.azion.com.br
    - www.exceda.com
    - under.com.br
    - www.gocache.com.br
    
