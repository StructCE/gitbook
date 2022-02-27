# Devise

## Autenticação

Não é novidade que os serviços de autenticação são cruciais para praticamente todos os websites modernos, principalmente para garantir o armazenamento dos dados de usuários ou limitar funcionalidades apenas a usuários autorizados.

No caso do rails, existem diversas gems que nos possibilitam o desenvolvimento de sistemas com autenticação, sendo o [devise](https://github.com/heartcombo/devise) a gem mais utilizada entre elas (mais de 400 mil usuários).

## Token

Como não trabalhamos com rails full-stack, para manter a referência do usuário e mantê-lo sempre logado iremos utilizar um **token de autenticação**, que será uma chave única passada no cabeçalho de todas as requisições, informando à api qual é o usuário que está logado.

Para isso, faremos o uso da gem [simple_token_authentication](https://github.com/gonzalo-bulnes/simple_token_authentication), que foi feita para funcionar com o devise e irá facilitar bastante essa parte de autenticação por token.

## Instalação

Assim como a maioria das gems, para começar a utilizar o devise, devemos adicioná-la ao nosso projeto, adicionando a linha `gem 'devise'` na Gemfile e rodando o comando `bundle` no diretório do projeto.

Em seguida, rode o comando `rails g devise:install` para instalar todos os arquivos do devise. Com o isso o devise já estará pronto para ser usado.

Além disso, como iremos realizar a autenticação por token, também precisaremos adicionar `gem 'simple_token_authentication'` à gemfile e rodar o bundle. 

## Uso

Iremos utilizar o devise para criarmos models de usuário que necessitem de autenticação, podendo ser uma model de cliente, de administrador, de moderador ou qualquer outra que nossa aplicação precise. 

Nesse tutorial, criaremos apenas uma model de usuário genérica _User_, mas é importante ressaltar que esse é apenas o nome de model que será utilizado nesse exemplo. Caso a sua model tenha outro nome, substitua, onde aparecer, a palavra user pelo nome de sua model.

### Model

Para criar a model com o devise, é como criar uma model normal, porém agora substituindo a palavra chave _model_ por _devise_ no comando:
```
rails g devise User
```

Esse comando irá criar a model User, que já terá automaticamente o campo _email_. Repare que a model não tem o campo de senha, apenas o campo _encrypted_password_, isso é para garantir que não seja possível visualizar a senha dos usuários que forem cadastrados em nossa aplicação.

Em seguida, podemos gerar uma migration nova para adicionar os campos que desejamos que o usuário tenha, como nome e idade, por exemplo.

```
rails g migration AddFieldsToUser name:string age:integer
rails db:migrate
```

Agora a tabela de usuário já deve estar em seu banco de dados, e já é possível criar uma instância de usuário dentro do console do rails, em que precisamos passar, além dos campos criados na migration acima, o email, senha e confirmação de senha do usuário, sendo que a senha deve ter no mínimo 6 caracteres.

```
rails c
User.create(name: 'Usuário Exemplo', email: 'exemplo@gmail.com', age: 18, password: '123456', password_confirmation: '123456')
```

Pronto, criamos nossa primeira instância da model de usuário, mas agora como fazer para descobrir se ele foi criado com a senha correta se não conseguimos ver isso na model? Para isso, podemos chamar o método _valid_password?_, que retornará true se a senha passada for a senha da model e false caso contrario.

```
User.last.valid_password?('123456')
```

Para a parte de autenticação por token, é necessário entrar no arquivo da model (models/user.rb) e adicionar a linha `acts_as_token_authenticatable`. Além disso, é necessário adicionar um campo na model para armazenar o token, que queremos que seja único e com o tamanho máximo de 30 caracteres, para isso iremos gerar uma nova migration.
```
rails g migration AddTokenToUser authentication_token:string{30}:uniq
rails db:migrate
```

Agora todos os usuários que forem sendo criados já terão um token atrelados e, caso já tenha criado algum usuário sem o token de authenticação, não é necessário excluí-lo de seu banco de dados, basta dar um update nas instâncias que ainda não possuem o token que ele será gerado automaticamente.
```
rails c
User.where(authentication_token: nil).each do |user|
    user.update(email: user.email)
end
```

### Controller

Com a model já criada, podemos criar uma controller versionada de usuários com `rails g controller api::v1::users` e dentro da controller vamos criar duas requisições básicas: login e logout.

#### Login

Para a função de login, devemos receber como parâmetro o email e a senha do usuário que está querendo logar e, caso encontremos um usuário com aquele email e a senha esteja correta, retorne um json com os dados do usuário.

```
def login
    user = User.find_by!(email: params[:email])
    if user.valid_password?(params[:password])
        render json: user, status: :ok
    else
        head :unauthorized
    end
rescue StandardError => e
    render json: { message: e }, status: :not_found
end
```

{% hint style="info" %} 
Você pode estar se perguntando como que essa função pode funcionar para o login, já que ela só retorna um json com os dados do usuário. A ideia é que, na integração com o React, pegaremos esses dados de usuário que foram retornados, salvaremos nos cookies do navegador (ou no async storage, no caso do react native) e, toda vez que fizermos alguma requisição para a api, iremos passar no header (cabeçalho) o email e o token de autenticação do usuário, informando para a api qual é o usuário que está logado.
{% endhint %}

#### Logout

Para a função de logout, é preciso que o usuário esteja logado anteriormente e usaremos o token de autenticação para esse efeito. Para isso, adicionamos na primeira linha da controller `acts_as_token_authentication_handler_for User, only: :logout`, que fará com que antes de ser executado o método de logout, seja verificado se o token e o email recebidos do cabeçalho são válidos para alguma instância da model de usuário. 

Perceba que com essa verificação antes do método, sempre que uma autenticação por token falhar, o rails será redirecionado para sua página inicial, que muitas vezes não é o comportamento desejado. Para evitar isso podemos simplesmente adicionar ao final dessa linha`, fallback_to_devise: false`, no entanto, o recomendado é criarmos um método próprio para lidar com essa falha na autenticação, em que podemos simplesmente renderizar uma mensagem de erro.
```
def authentication_failure
    render json: { message: 'Erro de autenticação!'}, status: :unauthorized
end
```

{% hint style="info" %} 
Esse método pode ser definido na própria controller do usuário ou até na application controller, no caso de uma aplicação com mais de uma model de usuário em que queremos reaproveitar os métodos
{% endhint %}

Em seguida, precisamos adicionar esse método nas rotas, então entre no arquivo *routes.rb* e adicione a linha 
```
get 'authentication_failure', to: 'application#authentication_failure', as: :authentication_failure
```

{% hint style="info" %}
Esse `as: :authentication_failure` na rota tem como função criar uma espécie de apelido para chamarmos essa rota dentro de nossa aplicação rails, assim, em qualquer lugar da aplicação, será possível redirecionar para rota por `redirect_to :authentication_failure_url`
{% endhint %}

Em seguida, iremos criar uma classe customizada para sobrescrever o método de redirecionamento da url de acordo com o tutorial da própria [Wiki do Devise](https://github.com/heartcombo/devise/wiki/How-To:-Redirect-to-a-specific-page-when-the-user-can-not-be-authenticated). Para criar essa classe, iremos criar no diretório *lib* o arquivo *CustomFailure.rb* e definimos a classe com
```
class CustomFailure < Devise::FailureApp
    def redirect_url
        authentication_failure_url
    end
end
```

Como o rails não carrega essa pasta automaticamente, devemos entrar no arquivo *config/application.rb* e adicionar a linha abaixo:
```
config.autoload_paths << Rails.root.join('lib')
```

Por fim, entre no arquivo *config/initializers/devise.rb*, procure pela parte do *Warden* que é o que faz a parte de login e adicione a linha abaixo para sobrescrever o método de falha com o seu método customizado
```
config.warden do |manager|
    manager.failure_app = CustomFailure
end
```

Agora já podemos fazer o nosso método de logout, que irá simplesmente apagar o token de autenticação do usuário atual
```
def logout
    current_user.update! authentication_token: nil
    render json: { message: 'Deslogado com sucesso!' }, status: :ok
rescue StandarError => e
    render json: { message e.message }, status: :bad_request
end
```

#### Passando o token no cabeçalho

Ao fazer uma requisição, seja pelo insomnia ou pelo react mesmo, temos a opção de passar um *header* para a requisição, em que iremos passar o email e o token do usuário que está logado. Para isso, vamos supor que eu fiz o login de um usuário com email **exemplo@gmail.com** e token de autenticação **abcd1234**. 
Com essas informações, entraremos no insomnia (ou thunder client, se preferir) e criaremos uma nova requisição (*Ctrl + N*) para o método de logout, que será um *post*, com a rota criada para a requisição, nesse exemplo será http://localhost:3000/logout. Agora abra a aba *Header* e adicione as linhas
```
X-User-Token: abcd1234
X-User-Email: exemplo@gmail.com
```
Agora já será possível testar o método de logout, ou qualquer outra requisição que precise de um usuário logado para funcionar.


#### Rotas

Após criarmos as requisições na controller, precisamos definir as rotas. Para isso, entre no arquivo _routes.rb_ e perceba que lá tem a linha `devise_for :users`, que define as rotas padrões do devise, que não precisaremos utilizar, mas que não podemos simplesmente apagar das rotas. Portanto, para não termos conflitos, modificamos essa linha para indicar que o usuário ainda vai ter os métodos do devise, porém as rotas não serão criadas.
```
devise_for :users, skip: :all
```

Agora já podemos criar as rotas normalmente
```
post 'logout', to: 'user#logout'
post 'login', to: 'user#login'
```
