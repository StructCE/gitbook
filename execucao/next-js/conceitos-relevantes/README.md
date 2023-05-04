## Separação cliente/servidor

Quando um usuário acessa uma _url_, uma request é feita para essa _url_, e então uma resposta é retornada.

Quando a _request_ chega no servidor, ela possui informações como headers, método http, rota, etc. O servidor pode então processar essa request. A gente escreve código para isso, e esse código será acessado somente no servidor. Isso significa que, nesse código, não existe a variável `window`, o console.log não vai aparecer no console do navegador, e sim no terminal que está rodando o servidor, etc.

Após receber a request, o servidor envia uma resposta, que pode incluir HTML, CSS, JS, imagens, pdfs, json, etc.
O JS enviado muitas vezes também é código escrito por nós, e nesse caso esse código será rodado no cliente apenas.

Isso significa que vão existir outras limitações, como impossibilidade de se acessar variáveis de ambiente, algumas api's do node não são padrões dos navegadores, etc.

## _assets_ estáticos

Um _asset_ estático nada mais é do que um objeto que é enviado para o cliente sem necessidade de alterar o objeto.

Ou seja, o objeto já existe no servidor, e então é apenas enviado como resposta. Pode ser, por exemplo: imagem, index.html, robots.txt, pdf, etc; desde que não seja alterado pelo servidor.

## Renderização

Começando com um exemplo:

Usando react, escrevemos uma função que retorna JSX. Ao rodar essa função, HTML é `renderizado`.

Em suma, renderização é gerar algo que pode ser mostrado na tela do navegador, como um HTML. Isso exige um processamento, ou seja, um custo de tempo, espaço e energia.

## SSR

É quando o servidor recebe uma request, renderiza um conteúdo, e envia para o cliente algo já renderizado.

## SG

É quando o servidor, no processo de build/compilação, renderiza um conteúdo e gera um _asset_ estático.

Agora, o servidor recebe uma request, e envia para o cliente algo já renderizado.

### ISR

É um híbrido entre o SSR e o SG, com alterações para encaixar os dois

Na primeira request que o servidor recebe, ele renderiza um conteúdo, e envia para o cliente algo já renderizado. Então, guarda o conteúdo renderizado.

Nas próximas requests, o servidor logo envia para o cliente algo já renderizado.

Geralmente existe um mecanismo para revalidar o conteúdo e rerenderizá-lo.
