# Geradores

Os geradores são linhas de código que nos ajudam a criar **models**, **controllers**, **serializers**, **migrations**, entre outros, que podem ser encontrados rodando um `rails generate` no terminal dentro de um projeto Rails, seja Full-Stack, seja API. É bom lembrar que podemos trocar o `generate` por apenas `g`, que usaremos ao longo dessa página, e teremos o mesmo resultado. Teremos o foco na geração de arquivos para Rails API, mas é bom lembrar que eles também funcionam para Rails Full-Stack com pouca ou nenhuma modificação.

## Geração de Model

Gerar uma model em um projeto Rails é muito simples e requer apenas uma linha, que se parece muito com:

```bash
rails g model <NomeDaModel> <campo>:<tipo>
```

Os tipos disponíveis são: `binary` para um BLOB (Binary Large OBject), `boolean` para booleano, `date` para data, `datetime` para data com hora, `decimal` ou `float` para números decimais, `integer` para inteiros, `primary_key` para uma chave primária única para cada elemento da tabela, `string` para textos pequenos, `text` para textos maiores, `time` para horários, `timestamp` para data com hora preenchida pela própria base de dados e `references` para referenciar outra model.

O `<NomeDaModel>` também pode ser escrito como `<nome_da_model>`, sempre no singular.

Após rodar o comando, por exemplo, `rails g model Country name:string population:integer`, aparecerão no terminal as seguintes linhas:

```bash
    invoke  active_record
    create    db/migrate/20210901212108_create_countries.rb
    create    app/models/country.rb
    invoke    rspec
    create      spec/models/country_spec.rb
    invoke      factory_bot
    create        spec/factories/countries.rb
```

Nesse caso, foram criadas uma **migration** na pasta **db/migrate**, um arquivo **country.rb** na pasta **app/models**, como o rspec já estava instalado, um arquivo de testes na pasta **spec/models** e, como o factory bot já estava instalado, uma factory na pasta **spec/factories**

Pronto, assim você terá gerado uma model.

## Geração de Controller

Para gerar uma controller, o comando é muito parecido com a model, porém, em vez de rodarmos um `rails g model`, rodaremos:

```bash
rails g controller <NomeDaController>
```

Como na Struct estamos usando Rails API, gostaríamos de versionar essa controller, uma vez que podemos mudar a API para outra versão no futuro. Para isso, mudaremos o código para:

```bash
rails g controller api::<versão>::<NomeDaController>
```

A versão é, normalmente `vx`, sendo `x` o número da versão da API.

Assim como na geração de models, o `<NomeDaController>` pode ser escrito como `<nome_da_controller>`, sempre no plural.

Após rodar o comando, por exemplo, `rails g controller api::v1::countries`, aparecerão no terminal as seguintes linhas:

```bash
    create  app/controllers/api/v1/countries_controller.rb
    invoke  rspec
    create    spec/requests/api/v1/countries_spec.rb
```

Nesse caso, será criada a controller **countries_controller.rb** na pasta **app/controllers/api/v1** e, com o rspec instalado, um arquivo de testes na pasta **spec/requests/api/v1**.

Desse modo, a controller estará pronta para ser preenchida.

## Geração de Serializer

A geração de serializer, que é a ferramenta que usamos para passar os parâmetros do JSON, é também muito simples, basta rodar:

```bash
rails g serializer <NomeDoSerializer>
```

Assim como em models e controllers, o `<NomeDoSerializer>` pode ser escrito como `<nome_do_serializer`, sempre no singular.

Após rodar, por exemplo, `rails g serializer Country`, o terminal nos devolve:

```bash
    create  app/serializers/country_serializer.rb
```

Isso significa que o serializer foi gerado na pasta **app/serializers**, pronto também para ser utilizado.

## Geração de Devise

O Devise é nossa gem para implementação de um sistema de usuários na nossa API. Após a instalação da gem do devise, o seu gerador segue o padrão dos outros:

```bash
rails g devise <NomeDaModel>
```

O nome da model é geralmente `User`, porém pode ser qualquer outra coisa, desde que seja em inglês.

## Geração de Migrations

### Migration de adição e remoção de coluna na tabela

Caso você tenha esquecido de adicionar uma coluna a uma model, você pode usar uma migration. A migration de adição é muito simples de ser criada, basta rodar um:

```bash
rails g migration Add<Coluna>To<Model> <campo>:<tipo>
```

Ou seja, caso tenhamos esquecido de adicionar a coluna língua para a model Country, podemos rodar `rails g migration AddLanguageToCountries language:string` e recebemos:

```bash
    invoke  active_record
    create    db/migrate/20210901220710_add_language_to_countries.rb
```

Que mostra que uma migration foi criada na pasta **db/migrate**, que terá um conteúdo parecido com isto:

```rails
class AddLanguageToCountries < ActiveRecord::Migration[6.0]
  def change
    add_column :countries, :language, :string
  end
end
```

Lembrando sempre que o `Add<Coluna>To<Model>` pode ser escrito como `add_<coluna>_to_<model>`, com a model no plural.

Caso tenha uma coluna que queira remover, é só trocar `Add` ou `add` por `Remove` ou `remove`, dependendo de como estiver escrevendo.

### Migration de criar tabela N-M

A tabela N-M é uma tabela associativa, ou seja, que associa, por exemplo, vários filmes a vários atores.

Para criar a tabela associativa do exemplo dado, usaremos `rails g migration CreateJoinTableMovieActor movie actor`

Esse método não é muito utilizado na Struct. Preferimos usar `rails g model MovieActor movie:references actor:references` para garantir a integridade do referencial.

### Migration genérica

Criar uma migration genérica é apenas utilizar `rails g migration <NomeDaMigration>`, sendo que o nome da migration deve ser uma ação para ser feita por ela, como `add_columns_to_human`. Isso gerará uma migration sem nada dentro a não ser sua classe e um `def change`.

## Destruindo uma geração

Não, essa não é a parte que fazemos um extermínio, é a parte que queremos reverter uma migration, uma controller, uma model, um serializer ou qualquer outra geração que tenhamos feito.

Para isso, usamos:

```bash
rails destroy <geração> <NomeDaGeração>
```

Podemos usar `rails destroy migration CreateJoinTableMovieActor` para destruir a migration que fizemos anteriormente antes de termos rodado um `rails db:migrate` ou um `rake db:migrate`.

Assim, cobrimos os geradores utilizados na Struct.