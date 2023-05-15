# Deploy

Deploy nada mais é do que colocar o seu projeto no ar, para que ele possa ser acessado por qualquer pessoa. Para tal, é utilizada um domínio que aponta para o endereço ip de um servidor, que é onde o projeto está hospedado. O servidor pode ser um computador pessoal, um servidor de hospedagem, um servidor de cloud, etc.

Em processo de [staging](https://pt.wikipedia.org/wiki/Ambiente_de_implanta%C3%A7%C3%A3o), é comum terceirizar e utilizar domínios temporários, usando como Heroku, Netlify, Railway, etc.

Para entender deploy é necessário entender o fluxo desencadeado ao entrar num site.

## Entrando num site

Quando entramos num site, o que acontece é o seguinte:

1. O navegador faz uma requisição (get '/', ou outra rota) para o domínio.
2. O domínio é encontrado (ou não) nas listas de autoridades de domínios. Ele aponta para o endereço ip do servidor, para o qual a requisição é direcionada.
3. O servidor responde com algo (html, css e js; um json; etc).

Então, precisamos definir o que é esse algo. Para isso, em serviços terceirizados geralmente são automatizados alguns processos (mas nem sempre), como:

- Instalação de dependências
- Compilação de arquivos
- Criação de assets estáticos (js bundles, css bundles, etc.)
- Criação de banco de dados

Permitindo que nossa aplicação rode e responda a requisições da mesma maneira que os faz em nossa máquina local (`localhost`).
