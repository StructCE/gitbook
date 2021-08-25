# Teste com Associatividade

Para essa página, levaremos em consideração que a construção de uma controller e de uma model já está bem clara e, então, passaremos direto por essa parte.

No nosso exemplo, precisaremos de uma model que está associada à outra, então, a ideia é que teremos uma model de **produtos** e cada produto tem uma model de **categorias**. Por exemplo, a **categoria** de bebidas pode ter diversos **produtos (1 categoria - N produtos)**.

Nossas models estarão assim:

Categoria:

```ruby
class Category < ApplicationRecord
    has_many :products
end
```

Produto:

```ruby
class Product < ApplicationRecord
  validates :name, :description, :price, presence: true
  validates_length_of :name, minimum: 3
  validates_length_of :description, minimum: 10
  validates :price, numericality: true
  belongs_to :category
end
```

Para o nosso exemplo, o factory_bot estará assim:

Categoria:

```ruby
FactoryBot.define do
  factory :category do
    name { "Bebidas" }
  end
end
```

Produto:

```ruby
FactoryBot.define do
  factory :product do
    name { "Rango muito bom" }
    description { "O rango mais maravilhoso de todos" }
    price { 20.0 }
    category { association :category }
  end
end
```

Como é percebível, essas factories são iguais a todas as que criamos nos exemplos anteriores a única diferença é que, na factory de produto, temos o campo **category { association :category }**, isso quer dizer que um produto precisa referenciar uma categoria e, essa categoria tá sendo associada ao campo por meio da factory category. Resumindo, é como se tivéssemos criado um produto e colocado ele na classe de bebidas.

## Testes de Models

Agora, tendo nossas models e nossas factories prontas, podemos começar testando as models. Para esse exemplo, testaremos a model de um método diferente que também é bastante usado.

```ruby
require 'rails_helper'

RSpec.describe Product, type: :model do
    describe 'factory' do 
      context 'when normal factory' do 
        it 'be valid' do 
          produto = build(:product)
          expect(produto).to be_valid
        end
      end
    end
end
```

Nessa forma de teste, quebramos em **describes** e cada **context** tem apenas um **it**. Dessa forma, é um teste mais direto, mas também pode ser um pouco mais complexo para quem não entende muito de Rspec.

No exemplo, só testamos se a **factory** do produto era funcional, esse teste vai nos retornar um caso de sucesso, agora precisaremos criar um describe para as validações da model.

```ruby
require 'rails_helper'

RSpec.describe Product, type: :model do
  describe 'factory' do 
    context 'when normal factory' do 
      it 'be valid' do 
        produto = build(:product)
        expect(produto).to be_valid
      end
    end
  end

  describe 'validations' do 
    context 'when product does not have a name' do 
      it { expect(build(:product, name: nil)).to be_invalid }
    end

    context "when product's name has less than 3 characters" do 
      it { expect(build(:product, name: 'oi')).to be_invalid }
    end

    context "when product does not have a description" do 
      it { expect(build(:product, description: nil)).to be_invalid }
    end

    context "when product's description has less than 9 characters" do 
      it { expect(build(:product, description: '123456789')).to be_invalid }
    end

    context "when product does not have a price" do 
      it { expect(build(:product, price: nil)).to be_invalid }
    end

    context "when product's price is not a number" do 
      it { expect(build(:product, price: 'asdasd')).to be_invalid }
    end

    context "when product does not have a category" do 
      it { expect(build(:product, category: nil)).to be_invalid }
    end
  end
end
```

Então, como podemos ver, fazemos um contexto para cada validação e os exemplos (it) são os próprios testes em si. Como dá para perceber, esses testes podem ser feitos em apenas uma linha, no **describe** da **factory** fazemos a mesma coisa que fazemos no **describe** das **validations** com a única diferença que as validações estão sendo verificadas de forma mais diretas, enquanto as factories são verificadas de forma mais descritiva.

## Testes de Controllers

Para o caso dos controllers, basicamente, a mesma coisa que os testes anteriores. No nosso caso, vamos levar em consideração que é uma api versionada.

Controllers:

```ruby
class Api::V1::ProductsController < ApplicationController
    def create 
        product = Product.new(product_params)
        product.save!

        render json: product, status: :created 
    rescue StandardError => e  
        head(:bad_request)
    end
    
    def index 
        products = Product.all 
        render json: products, status: :ok
    end

    def show 
        product = Product.find(params[:id])

        render json: product, status: :ok
    rescue StandardError => e  
        head(:bad_request)
    end

    def update 
        product = Product.find(params[:id])
        product.update!(product_params)

        render product, status: :ok 
    rescue StandardError => e  
        head(:bad_request)
    end

    def delete 
        product = Product.find(params[:id])
        product.destroy!

        render product, status: :ok
    rescue StandardError => e  
        head(:bad_request)
    end

    private 
    def product_params
        params.require(:product).permit(
            :name,
            :description,
            :price,
            :category_id
        )
    end
end
```

A gente percebe que, diferente de uma categoria normal, temos ali o campo category_id, esse é o mesmo campo que criamos na nossa factory de produtos para que o produto criado fosse um produto aceitável.

Rotas:

```ruby
Rails.application.routes.draw do
  namespace 'api' do 
    namespace 'v1' do 
      scope 'products/' do 
        get 'index', to: "products#index"
        post 'create', to: "products#create"
        get 'show/:id', to: "products#show"
        put 'update/:id', to: "products#update"
        delete 'delete/:id', to: "products#delete"
      end
    end
  end
end
```

Nesse caso, não vamos detalhar os testes como fizemos nos exemplos anteriores, pois, a partir desse ponto, espera-se que vocês já estejam entendendo como se faz um teste com Rspec, o nosso intuito é passar como fazer testes de uma model que tem associação com outra model.

```ruby
require 'rails_helper'

RSpec.describe "Api::V1::Products", type: :request do
    
  context 'GET /index' do
    it 'should render all products' do 
        get '/api/v1/products/index'
        expect(response).to have_http_status(:ok)
    end
  end

  context "POST /create" do 
    let(:categoria) {create(:category)}
    let(:produto) do 
        {name:'produto', description:'apenas um produto', price: 15.0, category_id: categoria.id}
    end

    it 'with valid params' do 
        post '/api/v1/products/create', params: {product: produto}
        expect(response).to have_http_status(:created)
    end

    it 'with invalid params' do
        produto = {name:''}
        post '/api/v1/products/create', params: {product: produto}
        expect(response).to have_http_status(:bad_request)
    end
  end

  context "GET /show" do
    it 'with existing product' do 
        produto = create(:product)
        get "/api/v1/products/show/#{produto.id}"
        expect(response).to have_http_status(:ok)
    end

    it 'with non existing product' do 
        get "/api/v1/products/show/2"
        expect(response).to have_http_status(:bad_request)
    end
  end

  context "PUT /update" do 
    let(:produto) {create(:product)}
    atualizado = {name:'suco de manga'}

    it 'should update info' do 
        put "/api/v1/products/update/#{produto.id}", params: {product: atualizado}
        produto.reload
        expect(response).to have_http_status(:ok)
        expect(produto.name).to eq(atualizado[:name])
    end

    it 'should not update info' do 
        put "/api/v1/products/update/2", params: {product: atualizado}
        produto.reload
        expect(response).to have_http_status(:bad_request)
    end
  end

  context "DELETE /delete" do 
    let(:produto) {create(:product)}
    it 'should delete' do 
        delete "/api/v1/products/delete/#{produto.id}"
        expect(response).to have_http_status(:ok)
    end

    it 'should not delete' do 
        produto.destroy!
        delete "/api/v1/products/delete/#{produto.id}"
        expect(response).to have_http_status(:bad_request)
    end
  end
end
```

Como podemos ver, é basicamente o teste de uma api versionada. A diferença tá no método create, que precisaremos passar uma categoria para ele na criação, ou seja, no campo **category_id**, adicionaremos o id da categoria que criamos por meio da nossa factory.

Caso rodemos o comando **rspec** no terminal, teremos como retorno:

`17 examples, 0 failures`

Ou seja, tanto nossos testes de model quanto os de controller estão funcionando normalmente.