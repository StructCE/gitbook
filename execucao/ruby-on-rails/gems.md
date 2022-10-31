# Gems

As *gems* do *Ruby on Rails* são bibliotecas externas que fornecem funcionalidades ao seu projeto. Dependendo do projeto em questão, os desenvolvedores precisarão utilizar gems que não vem configuradas por padrão em um projeto de *Ruby on Rails*, de forma que cabe ao gerente de projetos o trabalho de analisar quais gems serão necessárias no decorrer do projeto, colocar essas gems no `Gemfile` e realizar qualquer outra configuração para que essas gems funcionem adequadamente \(a maioria das gems requer alguma configuração adicional para funcionar\).

Além de configurar as novas gems, o gerente de projeto também deve verificar qualquer aviso de *deprecated gem* gerado pelo Rails após a execução dos comandos `bundle install` e `rails s` e corrigir esses avisos para evitar problemas com o projeto.

Idealmente, esse processo de configuração deve ser feito no *começo* do projeto para que todos os desenvolvedores tenham acesso às funcionalidades adequadas para o desenvolvimento do projeto \(e para que eles não tenham que ficar rodando `bundle install` toda hora\). Lembre-se de, após configurar ou substituir uma gem, sempre tentar executar o projeto com o comando `rails s` para garantir que o funcionamento do projeto não foi afetado por alguma gem mal configurada.

Para facilitar o uso dessa seção pelo gerente de projeto \(ou qualquer outro membro da Struct\), vamos dividir as gems que devem ser configuradas manualmente em duas seções: *gems essenciais* e *gems úteis*. Também vamos listar alguns casos comuns de *deprecated gems* que devem ser substituídas.

## Gems essenciais

As *gems essenciais* são gems que devem ser configuradas em **todos** os projetos da Struct de *Ruby on Rails*, por proporcionarem funcionalidades que são necessárias ou para o desenvolvimento do projeto ou para a garantia básica da qualidade do projeto. Como gerente de projeto, é sua responsabilidade incluir e configurar **todas** as gems dessa seção no projeto.


### RSpec

O RSpec é uma framework de testes utilizado para redigir testes de unidade e testes de módulo.

Para instalar e configurar o RSpec e o factory bot, siga os passos descritos nas páginas de [instalação do Rspec](../rspec-e-factory-bot/instalacao-rspec.md) e [de instalação do factory bot](../rspec-e-factory-bot/instalacao-factory-bot.md)

### Devise and Simple Token Authentication

Duas gems que trabalham juntas para a criação de um usuário com login funcional (com proteção de sua senha em um token).

Com a gem Devise é possível criar uma model especial (device) com todas as características para permitir a criação de um usuário, como e-mail e senha.

Já a gem Simple Token Authentication garante que o acesso a rota da controller seja permitido apenas por quem esteja com o token certo, ou seja, logado corretamente.

1. Adicione o trecho de código abaixo ao arquivo `Gemfile`:

```
gem 'devise'
gem 'simple_token_authentication'
```

2. Execute o comando `bundle install` para instalar as gem adicionadas ao `Gemfile`.

3. Execute o comando `rails g devise:install` para instalar todos os arquivos do devise.


### Rubocop

Rubocop é um analisador e formatador de código que serve para padronizar e
melhorar seu código como um todo.

Essa gem é bem flexível (podendo ser configurada e estilizada) e garante um código
mais limpo e organizado, já que os projetos são feitos em grupos e, assim, cada um
tem sua forma de organizar distinta.

1. Adicione o trecho de código abaixo ao arquivo `Gemfile`:

```
# Rubocop
gem 'rubocop', '~> 1.24.1', require: false
gem 'rubocop-rails', require: false
gem 'rubocop-rspec', require: false
```

2. Execute o comando `bundle install` para instalar as gem adicionadas ao `Gemfile`.

3. Rode o comando `robocop -A` no seu terminal do projeto para
executar a verificação de seu código.

  Note que, provavelmente, serão identificadas ofensas que podem não ser corrigidas automaticamente, sendo necessário concertá-las manualmente antes de ser feito o
  commit.

#### Regras do rubocop

Ao utilizar o rubocop, muito provavelmente você não vai querer utilizar todas as suas regras como padrão, já que em alguns casos vezes elas não fazem muito sentido ou são bem chatinhas e acabam atrapalhando mais do que ajudando. Nesses casos, você pode configurar desabilitar algumas regras por padrão e, para isso, basta criar na raíz do projeto o arquivo *.rubocop.yml*. Neste arquivo, primeiro adicione as seguintes linhas

```
require:
  - rubocop-rails
  - rubocop-rspec

  
AllCops:
  TargetRubyVersion: 2.7.2 # Mude para a sua versão do ruby
  NewCops: enable
  Exclude:
    - db/schema.rb
    - bin/bundle

Style/Documentation:
  Enabled: false

Style/FrozenStringLiteralComment:
  Enabled: false
```

Nesse trecho de código, estão sendo adicionadas as extensões *rubocop-rails* e *rubocop-rspec* (especificadas na gemfile), está sendo especificada a versão do ruby e habilitando os novos cops, o que será necessário para adicionar o rubocop ao CI no github, além disso, estão sendo excluídos alguns arquivos padrões do rails que podem dar problemas. caso queira ignorar um diretório inteiro, basta adicionar nessa lista ` - dir/**`.

As últimas duas configurações estão desabilitando o cop de documentação com comentário e desabilitando o cop de Strings literais imutáveis, que introduzem uma feature que não é utuilizada com frequência em Rails e que possui pouca aplicação no momento.

Além disso, algumas configurações do rubocop são em relação ao tamanho das coisas (métodos, classes, testes), nesse caso, é possível apenas alterar o limite máximo ao invés de desabilitar o cop, já que esses muita vezes são importantes. Por exemplo, para alterar o tamanho máximo dos métodos para 16 linhas, basta colocar 
```
Metrics/MethodLength:
  Max: 16
```

## Gems úteis

As *gems úteis* são gems que proporcionam funcionalidades desejáveis ou essenciais apenas em alguns casos, mas que não são necessárias em todos os projetos da Struct de *Ruby on Rails*. Como gerente de projeto, é sua responsabilidade ler a descrição das gems nessa seção e incluir e configurar apenas as gems que se apliquem ao projeto em questão.

### Figaro

O Figaro é uma gem utilizada para gerenciar credenciais de bancos de dados em um arquivo de configuração local. Recomenda-se sua utilização em projetos que possuam *um banco de dados com o SGBD \(Sistema gerenciador de banco de dados\) MySQL* ou qualquer outro SGBD que não possua um bom sistema de armazenamento de credenciais de login \(o PostgreSQL é um caso raro de SGBD que **não** precisa da gem Figaro\).

Para configurar o Figaro, siga os passos abaixo:

1. Adicione o trecho de código abaixo ao arquivo `Gemfile`:

  ```
  # Database credentials:
  gem 'figaro'
  ```

2. Execute o comando `bundle install` para instalar as gem adicionadas ao `Gemfile`.

3. Execute o comando `bundle exec figaro install` para configurar a gem.

4. Modifique o arquivo `config/database.yml` nas linhas demonstradas abaixo:

  ```
  default: &default
    # Modifique apenas as linhas abaixo e não apague ou modifique as outras linhas!
    username: <%= ENV['db_user'] %>
    password: <%= ENV['db_password'] %>
  ```

5. Adicione o trecho de código abaixo ao arquivo `config/application.yml`:

  ```
  # Database credentials:
  db_user: "seu_usuario_do_DB_entre_parentesis"
  db_password: "sua_senha_do_DB_entre_parentesis"
  ```

Após configurar a gem Figaro em seu ambiente, **avise os outros membros do projeto** que eles deveram executar os passos 2, 3 e 5 para configurar a gem em seus ambientes!


## *Deprecated* gems

As *deprecated gems* são gems que não recebem mais manutenção e suporte por parte de um time de desenvolvedores, devendo ser retiradas dos projetos da Struct de *Ruby on Rails*. Como gerente de projeto, é sua responsabilidade substituir todas as gems dessa seção que estão presentes no seu projeto.

### Chrome driver helper

A gem `chromedriver-helper` parou de receber suporte em Março de 2019. Substitua ela no Gemfile pela gem `webdrivers`.

### SASS Rails

A gem `sass-rails` parou de receber suporte em Março de 2019. Substitua ela no Gemfile pela gem `sassc-rails`.