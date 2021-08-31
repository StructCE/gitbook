# Geradores

Os geradores são linhas de código que nos ajudam a criar **models**, **controllers**, **serializers**, **migrations**, entre outros, que podem ser encontrados rodando um `rails generate` no terminal dentro de um projeto Rails, seja Full-Stack, seja API. É bom lembrar que podemos trocar o `generate` por apenas `g`, que usaremos ao longo dessa página, e teremos o mesmo resultado. Teremos o foco na geração de arquivos para Rails API, mas é bom lembrar que eles também funcionam para Rails Full-Stack com pouca ou nenhuma modificação.

## Geração de Model

Gerar uma model em um projeto Rails é muito simples e requer apenas uma linha, que se parece muito com:

```bash
rails g model <NomeDaModel> <campo>:<tipo>
```

Os tipos disponíveis são: `binary` para um BLOB (Binary Large OBject), `boolean` para booleano, `date` para data, `datetime` para data com hora, `decimal` ou `float` para números decimais, `integer` para inteiros, `primary_key` para uma chave primária única para cada elemento da tabela, `string` para textos pequenos, `text` para textos maiores, `time` para horários, `timestamp` para data com hora preenchida pela própria base de dados e `references` para referenciar outra model.

O `<NomeDaModel>` também pode ser escrito como `<nome_da_model>`, sempre no singular.

Após rodar o comando, por exemplo, `rails generate model Country name:string population:integer`, aparecerão no terminal as seguintes linhas:

```bash
    invoke  active_record
    create    db/migrate/20130715174248_create_countries.rb
    create    app/models/country.rb
    invoke    rspec
    create      rspec/models/country_spec.rb
```

Nesse caso, foram criadas uma **migrate** na pasta **db**, um arquivo **country.rb** na pasta **app/models** e, como o rspec já estava instalado, um arquivo de testes na pasta **rspec/models**.

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

