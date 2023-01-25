# Heroku


No momento da atualização dessa documentação, não existe mais plano grátis no Heroku. Como a gente é muito mão de vaca, não usamos mais. Mas caso necessário, basta usar a conta da struct e seguir os passos abaixo.
(Documentação atual feita pensada em Rails)

## O que é?
Heroku é uma plataforma de deployment de website, desenvolvidos em quase todos frameworks mais famosos utimamente, ela automaticamente analisa o repositório e verifica a linguagem que você está utilizando, e já faz o setup completo, facilitando uma das principais e mais demoradas atividades de um projeto de website.

O heroku roda um container docker com seus scripts de inicialização. Isso significa que é necessário que o seu projeto seja um servidor, ou seja, que ele tenha uma porta para ser acessado, e que ele seja capaz de responder a requisições. Sendo assim, é ideal para api's, mas não para servir _assets estáticos_ (como os gerados numa aplicação React comum).


## Como subir o site no heroku?


### Preparando o projeto


Crie uma branch chamada heroku, caso ainda não tenha, e faça as seguintes mudanças:

1. Crie um arquivo chamado `start.sh` na raíz do projeto com o seguinte conteúdo:

```sh
#!/bin/sh
rails db:migrate
bundle exec puma -C config/puma.rb
```

`#!/bin/sh`: essa linha tem, por principal objetivo, informar ao shell qual intérprete deverá ser usado para a execução do script. No nosso caso, o intérprete usado será o sh, ou seja o Bourne shell.

`rails db:migrate`: a linha de código padrão para executar as migrations no rails e garantir que todos os bancos de dados estejam atualizados e com suas informações certas


`bundle exec puma -C config/puma.rb`: esse código funciona como um rails s, ou seja, serve para executar o puma (servidor padrão do rails) com alguns recursos a mais que o rails s por si só, não oferece.


2. Caso seu projeto utilize Active Storage, ou guarda alguma imagem enviada por upload, é necessário mudar onde os arquivos ficam armazenados, escolhendo entre [cloudinary](https://cloudinary.com/documentation/ruby_rails_quickstart) e [amazon s3](https://devcenter.heroku.com/articles/active-storage-on-heroku). Em resumo, deve ser configurado os arquivos:

ATENÇÃO: Não colocar as chaves de acesso no repositório, apenas no heroku. Na branch de produção, requerer as variáveis de ambiente no heroku, e colocar no código com `ENV['NOME_DA_VARIAVEL']`. Por exemplo
```ruby
# NÃO FAZER ISSO NUNCA!!!!!!!! 
Cloudinary.config_from_url("cloudinary://API_KEY:API_SECRET@CLOUD_NAME")

# No lugar disso, fazer:
Cloudinary.config_from_url("cloudinary://#{ENV['CLOUDINARY_API_KEY']}:#{ENV['CLOUDINARY_API_SECRET']}@#{ENV['CLOUDINARY_CLOUD_NAME']}")
# E colocar as variáveis de ambiente no heroku
```

- `Gemfile` (instalar a SDK do serviço escolhido, depois rodar bundle);
- `config/environments/production.rb`;
- `config/storage.yml`;
- `config/initializers/active_storage.rb`.
Além de precisar colocar as chaves de acesso do serviço escolhido, lá no heroku.


### Subindo o projeto

#### Por CLI (Command Line Interface)
(Essa parte da documentação foi feita há bastante tempo por Pedro Augusto Ramalho Duarte)
- Se for sua primeira fez, siga o tutorial para instalar o cli do heroku https://devcenter.heroku.com/articles/heroku-cli#download-and-install
- Vídeo tutorial: https://youtu.be/V8wGbZOAe38
- Depois basta logar no heroku e criar um novo app.
- Na pasta do repositório do projeto, digite o comando ```heroku git:remote -a nome_do_app```
- Configure o banco de dados para postgresql
- E por fim rode o comando ```git push heroku master```

#### Por Dashboard

Acesse a dashboard da conta de projetos da Struct e crie um novo app. Em seguida, vá até a aba Deploy e selecione a opção GitHub. Selecione o repositório do projeto, escolha a branch `heroku` e clique em Deploy Branch. O deploy será feito automaticamente.

## Observação:

É possível usar do Heroku para fazer deploy de front-end. Basta criar um único endpoint para enviar os assets estáticos do front. Exemplo:


```js
// /package.json

{
  "scripts": {
    "build": "um comando de build qualquer", // comando para gerar os assets estáticos
    "start": "node server.js" // comando para rodar o servidor que servirá os assets
  }
}


```

```js
// /server.js

const express = require("express");
//chamamos o express para o arquivo

const { resolve } = require('path')
//para garantir que pegaremos o path exato

const app = express();
//criamos uma aplicação com o express

app.use("/", 
  express.static(
    resolve(
      __dirname,
      './build' // Onde os assets estáticos do front-end estão depois de rodar yarn build
    )
  )
);
//serve para pegarmos os itens de forma estática e servirmos o build

app.listen(process.env.PORT || 3000, (err) => {
  //usaremos a porta que o heroku definir ou a 300
  if (err) {
    return console.log(err);
  }
  //caso tenha um erro vai retornar o erro na callback
  console.log("Deu bom!");
  //no mais, esse console.log aparecerá na tela
});
```

Agora temos uma api, e então o deploy pode ser feito no Heroku.
