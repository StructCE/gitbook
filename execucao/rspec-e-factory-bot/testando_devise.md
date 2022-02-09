# Testando as models e controllers associadas ao Devise

Para testar as models associadas ao Devise, vamos usar como exemplo a model User:

`rails g devise User name:string`

Lembre-se de fazer a migração:

`rails db:migrate`

Se você fez a instalação do rspec e do factory-bot corretamente como descrita nos passos [Instalação do rspec](instalacao-rspec.md) e [Instalação do Factory Bot](instalacao-factory-bot.md), então na pasta **rspec/factories** deve ter sido criado o arquivo **users.rb** e na pasta **rspec/models** criado o arquivo **user_spec.rb**. 

Com isso, fazemos como nas outras models, com o [uso do factory bot](uso-do-factory-bot.md), para criar um default User:

```ruby
FactoryBot.define do 
    factory :user do 
        name { 'teste' }
        email { 'email@teste.com' }
        password { '12345678' }
        password_confirmation { '12345678' }
    end
end
```

Observe que precisamos colocar um email e senha que são obrigatórias para uma model do Devise.

Feito isso, podemos começar a testar a model no **user_spec.rb** como foi feito anteriormente:

```ruby
RSpec.describe User, type: :model do
  describe 'factory' do
    context 'when using standard factory' do
      it { expect(build(:user)).to be_valid }
    end
  end

  describe 'validations' do
    context 'when user does not have an email' do
      it { expect(build(:user, email: nil)).not_to be_valid }
    end
  end
end
```

A partir disso, podemos adicionar outras validações que dependerão das validations da model User(no arquivo **app/models/user.rb**), como **presence** do **name**:

`validates :name, presence: true`

Dessa forma:

```ruby
RSpec.describe User, type: :model do
  describe 'factory' do
    context 'when using standard factory' do
      it { expect(build(:user)).to be_valid }
    end
  end

  describe 'validations' do
    context 'when user does not have an email' do
      it { expect(build(:user, email: nil)).not_to be_valid }
    end

    context 'when user does not have a name' do
      it { expect(build(:user, name: nil)).not_to be_valid }
    end

  end
end
```

Para testarmos controllers, será necessário adicionar no arquivo **rails_helper.rb** criado automaticamente na própria pasta **rspec** as seguintes linhas dentro do bloco `RSpec.configure do |config|`:

```ruby
    # Devise Test helpers
    config.include Devise::Test::ControllerHelpers, type: :controller
    config.include Devise::Test::IntegrationHelpers, type: :request
```

Assim, o bloco `RSpec.configure do |config|` deve ficar mais ou menos assim: 

```ruby
    RSpec.configure do |config|
        # Remove this line if you're not using ActiveRecord or ActiveRecord fixtures
        config.fixture_path = "#{::Rails.root}/spec/fixtures"

        # If you're not using ActiveRecord, or you'd prefer not to run each of your
        # examples within a transaction, remove the following line or assign false
        # instead of true.
        config.use_transactional_fixtures = true

        # You can uncomment this line to turn off ActiveRecord support entirely.
        # config.use_active_record = false

        # RSpec Rails can automatically mix in different behaviours to your tests
        # based on their file location, for example enabling you to call `get` and
        # `post` in specs under `spec/controllers`.
        #
        # You can disable this behaviour by removing the line below, and instead
        # explicitly tag your specs with their type, e.g.:
        #
        #     RSpec.describe UsersController, type: :controller do
        #       # ...
        #     end
        #
        # The different available types are documented in the features, such as in
        # https://relishapp.com/rspec/rspec-rails/docs
        config.infer_spec_type_from_file_location!

        # Filter lines from Rails gems in backtraces.
        config.filter_rails_from_backtrace!
        # arbitrary gems may also be filtered via:
        # config.filter_gems_from_backtrace("gem name")

        # Devise Test helpers
        config.include Devise::Test::ControllerHelpers, type: :controller
        config.include Devise::Test::IntegrationHelpers, type: :request
    end
```
Agora podemos começar a montar os testes das nossas controllers.

Suponha que na sua aplicação o usuário(user) tenha produtos favoritos que ele quer adicionar para poupar tempo. Dessa forma, na controller de favoritos, você pode querer colocar uma função para ver favoritos e outra para criar favoritos:

```ruby
class Api::V1::FavouriteController < ApplicationController
  acts_as_token_authentication_handler_for User

  def index
    favourites = current_user.favourites
    render json: favourites, status: :ok
  end

  def create
    favourite = Favourite.new(favourites_params)
    if current_user.id === favourite.user_id then
      favourite.save!
      render json: favourite, status: :created
    elsif favourite.user_id === nil then
      render json: {message: "unprocessable_entity" }, status: :unprocessable_entity
    else
      render json: { message: "Você não pode criar um favorito para outro usuário" }, status: :unauthorized
    end
  rescue StandardError => e
    render json: {message: e.message}, status: :unprocessable_entity
  end
end
```
Como iríamos testar esses métodos se eles requerem o user estar logado? A resposta é simples: precisamos criar o user e usar o token e o email dele nos **headers** quando chamar o get/post:

```ruby
describe "/GET #index" do
    let(:user) { create(:user) }
    let(:product) { create(:product) } 
    before do
      create(:favourite, user: user, product: product)
      create(:favourite, user: user, product: product)
    end

    context 'logged in as user'
      before do
        get '/api/v1/favourites/', headers: {
          'X-User-Token': user.authentication_token,
          'X-User-Email': user.email
        }
      end
      it { expect(response).to have_http_status(:ok) }

      it 'returns with json' do
        expect(response.content_type).to eq('application/json; charset=utf-8')
      end

      it 'returns 2 elements' do
        expect(JSON.parse(response.body).size).to eq(2)
    end
end
```

E a mesma coisa faríamos para testar o método post:

```ruby
...
let(:user) { create(:user) }

let(:product) { create(:product) }

let(:params) do {
  product_id: product.id,
  user_id: user.id
}
end

context 'logged in as user with valid params' do
  before do
    post "/api/v1/favourites/create", params: { favourite: params }, headers: {
      'X-User-Token': user.authentication_token,
      'X-User-Email': user.email
    }
  end

  it { expect(response).to have_http_status(:created) }

  it 'creates the favourite' do
    new_favourite = Favourite.find_by(user_id: user.id, product_id: product.id)
    expect(new_favourite).not_to be_nil
  end
end
...
```

E quando o user não está logado, como testamos a falha na autenticação?

```ruby
context 'not logged in as user' do
  before do
    post "/api/v1/favourites/create", params: { favourite: params }
  end

  it 'returns a failure response' do
    expect(response).to redirect_to authentication_failure_path
  end
end
```

Como mostrado, usamos o **authentication_failure_path** que criamos na [configuração do devise](../devise.md). Dessa forma, como no post não foram informados o token e o email do user, a resposta foi redirecionada para o authentication_failure_path e no teste conseguimos testar isso também.
