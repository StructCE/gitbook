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

Iremos utilizar o devise para criarmos models de usuário que necessitem de autenticação, podendo ser uma model de cliente, de administrador, de moderador ou qualquer que outra que nossa aplicação precise. 

Nesse tutorial, criaremos apenas uma model de usuário genérica _User_, mas é importante ressaltar que esse é apenas o nome de model que será utilizado nesse exemplo. Caso a sua model tenha outro nome, substitua onde aparecer a palavra user, pelo nome de sua model.

### Model

Para criar a model com o devise, é como criar uma model normal, porém agora substituindo a palavra chave _model_ por _devise_ no comando:
```
rails g devise User
```

esse comando irá criar a model User, que já terá automaticamente os campo _email_. Repare que a model não tem o campo de senha, apenas o campo _encrypted_password_, isso é para garantir que não seja possível visualizar a senha dos usuários que forem cadastrados em nossa aplicação.

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

Com a model já criada, podemos criar uma controller versionada de usuários com `rails g controller api::v1::users` e dentro da controller vamos criar uma função de cadastro, uma de login e outra de logout. 


#### Login

Para a função de login, devemos receber como parâmetro o email e a senha do usuário que está querendo logar e, caso encontremos um usuário com aquele email e a senha esteja correta, retorne um json com os dados do usuário.

```
def login
    user = User.find_by!(email: params[:email])
    if user.valid_password?(params[:password])
        render json: user
    else
        head :unauthorized
    end
rescue StandardError => e
    render json: { message: e }, status: :not_found
end
```

#### Rotas

Após criarmos as requisições na controller, precisamos definir as rotas. Para isso, entre no arquivo _routes.rb_ e perceba que lá tem a linha `devise_for :users`, que define as rotas padrões do devise, que não precisaremos utilizar, mas que não podemos simplesmente apagar das rotas. Portanto, para não termos conflitos, modificamos essa linha para indicar que o usuário ainda vai ter os métodos do devise, porém as rotas não serão criadas.
```
devise_for :users, skip: :all
```

Agora já podemos criar as rotas normalmente
```
post 'signup', to: 'user#signup`
post 'logout', to: 'user#logout'
get 'login', to: 'user#login'
```