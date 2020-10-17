# Dados Estruturados

Dados estruturados são metadados contidos em elementos HTML na forma de tags e atributos com padrões específicos. Eles permitem que outros websites implementem funcionalidades através desses metadados e ajudem os mecanismos de busca e as demais aplicações que lidam com os dados web a identificar o conteúdo presente nas páginas. Um exemplo da utilidade de um dado estruturado é a imagem associada a um site no compartilhamento de um link por WhatsApp.

## Protocolo Open Graph

O Open Graph é um protocolo de código aberto que tem como intuito deixar os conteúdos nas redes sociais mais ricos. Através da adição de meta tags no código do site, é possível indicar uma série de dados sobre o conteúdo a ser exibido, como por exemplo qual imagem representerá a página ao ser compartilhado o URL da mesma.

### Sintaxe

A implementação do protocolo Open Graph pode ser feita através de tags `<meta>` na seção `<head>` do arquivo html. A sintaxe segue o modelo:

- Título: `<meta property="og:title" content="Título aqui" />`
- Descrição: `<meta property="og:description" content="Descrição a respeito da página" />`
- Imagem: `<meta property="og:image" content="https://site-da-imagem.com/imagem/foto.jpg" />`

Esses são os principais atributos, no entanto há outros que podem ser utilizados. Caso deseje saber mais a respeito do Open Graph, é possível encontrar mais informações no [site oficial do Open Graph](https://ogp.me/).
