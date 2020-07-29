# O que é CI/CD?
O Continuous Integration (CI), é um conjunto de regras de integração de código automatizadas, por exemplo, toda vez que uma pessoa der 
um commit/merge para develop, é rodado um linter para verificar se o código está no padrão, caso não esteja o commit/merge 
é automaticamente cancelado. Já no caso do Continuous Delivery(CD), é o mesmo princípio, só que para deploy do website, 
por exemplo, toda vez que der commit/merge na master o site é publicado no heroku.

# Como eu posso criar essas regras?
Existem várias ferramentas no mercado, no nosso caso utilizamos o gitlab ci/cd.

# Pré-requisitos?
- Projeto criado no heroku
- Banco de dados postgresql para publicar no heroku sem maiores problemas
- Rubocop no projeto (Caso não queira o rubocop, só excluir a regra respectiva)

## Passo a passo
1- Coloque o seguinte arquivo com o nome ```.gitlab-ci.yml``` na pasta root do seu projeto

```
before_script:
  - echo "deb http://toolbelt.heroku.com/ubuntu ./" > /etc/apt/sources.list.d/heroku.list
  - wget -O- https://toolbelt.heroku.com/apt/release.key | apt-key add -
  - apt-get update
  - apt-get install -y heroku-toolbelt
  - gem install dpl
  - gem install bundler -v 2.0.1
  - bundle install

rubocop:
  script:
    - bundle exec rubocop
  only:
    - development
    - master

production:
  stage: deploy
  variables:
    HEROKU_API_KEY: $HEROKU_PRODUCTION_API_KEY
  script:
    - dpl --provider=heroku --app=$HEROKU_APP_NAME --api-key=$HEROKU_API_KEY
    - heroku run rake db:migrate --exit-code --app $HEROKU_APP_NAME
  only:
    - master

```
{% hint style="info" %}
No before_script ele instala o necessário para rodar o projeto, e nos passos seguintes são as etapas de CI/CD que 
podem ser modificadas de acordo com a necessidade individual de cada projeto, no nosso caso o padrão rodará rubocop nos 
merge para master develop e deploy no heroku quando o merge for para master
{% endhint %}

2- Configurar as variáveis  em Settings/"CI/CD"/Variables
    - ```$HEROKU_PRODUCTION_API_KEY``` é uma chave que pode ser localizada nas configurações do heroku
    - ```$HEROKU_APP_NAME``` é o nome do seu app no heroku

3- Pronto seu CI/CD já está configurado para uso!!