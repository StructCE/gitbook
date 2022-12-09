# Heroku


No momento da atualização dessa documentação, não existe mais plano grátis no Heroku. Como a gente é muito mão de vaca, não usamos mais. Mas caso necessário, basta usar a conta da struct e seguir os passos abaixo.

## O que é?
Heroku é uma plataforma de deployment de website, desenvolvidos em quase todos frameworks mais famosos utimamente, ela automaticamente analisa o repositório e verifica a linguagem que você está utilizando, e já faz o setup completo, facilitando uma das principais e mais demoradas atividades de um projeto de website.

O heroku roda um container docker com seus scripts de inicialização. Isso significa que é necessário que o seu projeto seja um servidor, ou seja, que ele tenha uma porta para ser acessado, e que ele seja capaz de responder a requisições. Sendo assim, é ideal para api's, mas não para servir _assets estáticos_ (como os gerados numa aplicação React comum).


## Como subir o site no heroku?



- Se for sua primeira fez, siga o tutorial para instalar o cli do heroku https://devcenter.heroku.com/articles/heroku-cli#download-and-install
- Depois basta logar no heroku e criar um novo app.
- Na pasta do repositório do projeto, digite o comando ```heroku git:remote -a nome_do_app```
- Configure o banco de dados para postgresql
- E por fim rode o comando ```git push heroku master```

### Vídeo tutorial
- https://youtu.be/V8wGbZOAe38


## Observação:

Boa parte dessa documentação foi produzida por Pedro Augusto Ramalho Duarte, um ex-membro da Struct. Atualmente não estamos mais usando o Heroku, e por isso o tutorial pode estar desatualizado.
