# Início do projeto

O primeiro passo em um projeto de software consiste na criação e configuração do repositório em que o projeto será desenvolvido. Isso inclui criar o repositório do projeto, as estruturas de pastas para abrigar o código fonte e outros recursos e configurar adequadamente os arquivos de controle de versão, os arquivos de documentação do projeto, a utilização de bibliotecas externas \(gems\), e o banco de dados do projeto.

Embora isso pareça ser muita coisa, iremos detalhar melhor cada passo nas seções abaixo.

## Projeto Rails

O primeiro passo na inicialização do projeto é a criação do projeto na framework [*Ruby on Rails*](../ruby-on-rails/README.md). Para isso, vamos escolher, utilizando o RVM ou Rbenv, uma versão de Ruby esteja um *minor release* atrás da última versão \(ou seja, se a última versão de Ruby é a 2.x, utilize a versão 2.x-1 para o projeto\). Na dúvida, utilize a versão de Ruby utilizada no último projeto. Isso evita que tenhamos que lidar com os bugs inerentes à versão mais nova do Ruby e das gems que o acompanham. Caso algum dos membros do projeto não tenha um gerenciador de versão de Ruby instalado \(como RVM e Rbenv\), ajude ele com a instalação \(esse tipo de software é praticamente essecial para se trabalhar em vários projetos, cada um com uma versão diferente de Ruby\).

Após escolher a versão de Ruby desejada, será necessário realizar a instalação de algumas gems \(que são as bibliotecas do Ruby\). Para instalar uma gem, basta adicionar a gem ao arquivo Gemfile e rodar o comando `bundle install`. Com isso em mente, instale o *rails* \(framework de desenvolvimento de websites e serviços web\) e para o banco de dados, escolha entre o *mysql2* e o *pg*, gems para o MySQL e PostgreSQL respectivamente, os sistemas gerenciadores de bancos de dados, ou SGBDs, mais utilizados\). Além dessas gems, será necessário instalar os SGBDs MySQL e PostgreSQL em seu sistema operacional \(assunto que **não** será coberto nessa página\).

Após instalar as gems e os SGBDs em seu computador, caberá a você, como gerente de projetos, decidir qual SGBD utilizar no projeto. O MySQL é mais amigável para iniciantes e possui uma melhor forma de visualizar e manipular diretamente o banco de dados, mas requer mais tempo para ser configurado e a utilização de uma gem \([*figaro*](../../ruby-on-rails/gems.md#figaro)\) para gerenciar os credenciais de login. Já o PostgreSQL pode ser utilizado com quase nenhuma configuração adicional, mas possui uma instalação mais complicada e não permite que o usuário manipule o banco de dados com facilidade. Caso seja sua primeira vez gerenciando um projeto, fale com o diretor de projetos ou com um membro mais experiente para pedir uma recomendação \(eu, pessoalmente, recomendaria o PostgreSQL\).

{% hint style="info"%}
Para aprender um pouco mais sobre instalação do ruby e do rails e como configurar o banco de dados, confira os nossos [guias](../../../gestao/processo-seletivo/guias-utilizados.md).
{% endhint %}

Após escolher o SGBD a ser utilizado, chegou a hora de criar o projeto. Para isso, rode o comando `rails new nome_do_projeto_em_snake_case -d {mysql | postgresql} --api`, escolhendo o penúltimo argumento para coincidir com o SGBD desejado. O framework cuidará da criação de pastas e arquivos para o desenvolvimento do projeto.

Caso você tenha escolhido o MySQL, configure a gem [*figaro*](../../ruby-on-rails/gems.md#figaro) para gerenciar credenciais e, caso você **não** queira utilizar o usuário *root* no projeto, crie as tabelas de desenvolvimento e testes e um usuário com permissão de acesso a elas. Caso você tenha escolhido o PostgreSQL, preencha o arquivo `config/database.yml` com os credenciais do SGBD \(em sistemas operacionais com o *kernel* Linux, você pode preencher apenas o seu nome de usuário e apagar o campo de senha caso você tenha optado, na instalação do PostgreSQL, por utilizar sua conta de usuário do sistema operacional como um usuário do SGBD\).

Por fim, tente executar o projeto utilizando o comando `rails s`. Caso a execução do projeto não gere alguma mensagem de erro, adicione todos os arquivos gerados ao controle de versão sob o nome 'Commit inicial'. Caso contrário, corrija os erros do projeto **antes** de realizar o commit inicial.


## Segundo commit

Após a criação do repositório, você deverá fazer um segundo commit na branch main que faça todas as configurações necessárias no projeto. Esse segundo commit deve colocar no README informações básicas do projeto, colocar no projeto arquivos padrão que devem estar presentes em qualquer projeto da Struct e configurar as gems que o projeto irá utilizar (confira as [gem essenciais](../../ruby-on-rails/gems.md#gems-essenciais) para um projeto). Mais detalhes são fornecidos nas subseções abaixo. Após executar **todos** esses passos, realize um commit com o nome "Estrutura inicial" adicionando as mudanças que você fez.

### README

O README deve conter as dependências do projeto \(versão do Ruby, banco de dados, etc...\) e os dados do projeto em si, os quais incluem a especificação do projeto \(bem resumida, em uma única frase\), o codinome do projeto \(se existir\), a data de assinatura do contrato, o prazo de desenvolvimento do projeto e a data prevista de entrega do projeto.

Não utilize o README como uma lista de tarefas, pois isso pode ser feito por meio de *issues*.

### Arquivos padrão

No momento, existem 2 arquivos padrão que devem estar presentes no projeto: o `.gitignore` e o script `start.sh`.

#### Arquivo .gitignore

Como sabemos, o `.gitignore` é utilizado para impedir que arquivos locais sejam acidentalmente adicionados ao repositório. Arquivos que geralmente devem ser ignorados incluem arquivos de configurações pessoais \(`.bundle`, `.vscode`, `.idea`, `.DS_store`\), pastas de caches \(`tmp` e `storage`\), logs \(arquivos `*.log` e pasta `log`\) e módulos do *node js* \(a pasta `node_modules`\).

**Nunca** coloque arquivos que afetam o desenvolvimento do projeto \(como `Gemfile`\) no `.gitignore`.

É **essencial** que a configuração do `.gitignore` seja feita no **início** do projeto, pois problemas relacionados a esse arquivo são um pesadelo para serem resolvidos.

Segue, abaixo, um template de arquivo `.gitignore`:

```
# Environment normalization:
*.DS_Store
.idea
.rvmrc
.vscode
/.bundle
/vendor/bundle

# Ignore all logfiles and tempfiles:
/log/*
/tmp/*
!/log/.keep
!/tmp/.keep

# Ignore uploaded files in development:
/storage/*
!/storage/.keep

# Ignore node_modules:
node_modules/

# Ignore yarn files:
/yarn-error.log
yarn-debug.log*
.yarn-integrity

# Ignore precompiled javascript packs:
/public/packs
/public/packs-test
/public/assets

# Ignore Byebug command history file:
.byebug_history

# Ignore project secrets:
/config/initializers/secret_token.rb
/config/master.key
```

#### Arquivo start.sh

O arquivo `start.sh` é um script de execução utilizado para o *Docker*, servindo principalmente para que possamos fazer o deploy de nossa aplicação, mas que também pode ser utilizado para que novos integrantes do projeto inicializem o projeto sem maiores dificuldades.

Segue, abaixo, um template de arquivo `start.sh`:

```
#!/bin/sh
rails db:migrate
bundle exec puma -C config/puma.rb
```