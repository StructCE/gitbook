# O que é?

Next js é um _framework full stack_ construído em cima do React, da mesma maneira que React é construído em cima do JS. Por isso é muito simples nos adaptarmos e até usarmos a documentação do react normal para boa parte dos problemas enfrentados.

## Por que usar?

SG (_Static Generation_) e SSR (_Server Side Rendering_) ajudam muito na performance e no SEO (_Search Engine Optimization_) do web app.

Além disso, o diferencial do Next é o ISR (_Incremental Static Regeneration_), ou seja, o Next pode gerar páginas estáticas novas caso necessário. Ou seja, a página é renderizada no servidor uma vez quando surgir a primeira request para ela, e então é guardada em cachê como um _asset_ estático. Essa rota pode ser revalidada para gerar um novo _asset_ estático a ser guardado, caso necessário.

## Diferença principal do nosso React "padrão"

A diferença principal entre o Next e o Create React App (que normalmente usamos em projetos React):

SG (_Static Generation_) e SSR (_Server Side Rendering_) do diretório '/pages'

Geração de rotas a partir da organização de arquivos do diretório '/pages'

Capacidade de dar uma resposta de api (ou seja, com um json), desde que seja feito dentro do diretório 'pages/api/'
