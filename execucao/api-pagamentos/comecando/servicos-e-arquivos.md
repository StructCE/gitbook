Nem todas as lógicas de negócio encaixam nos moldes de uma Controller específica, e nem todas são facilmente implementadas em uma Model. Com a intenção de encapsular os métodos que chamarão a API e evitarmos redundância no código, estaremos os agrupando em objetos de Serviço. 

Um objeto de Serviço não é nada mais que um arquivo .rb em um diretório específico - o diretório *services*. Caso ainda não exista, criaremos o diretório no path *app/services*. Dentro do diretório, iremos separar nossos Serviços em módulos. Para fins de simplicidade, criaremos um módulo de pagamento que iremos utilizar para fazer a comunicação com o [Pagar.me](http://Pagar.me). Como exemplo, para termos um módulo *Payment*, criaremos o path *app/services/payment.*

Iremos dedicar esse módulo para os métodos que realizarão a comunicação com a API do Pagar.me - enviando requests e recebendo respostas. O arquivo .rb presente neste módulo atua como um intermediário entre a API do Rails e a API do Pagar.me - um *proxy.* Neste exemplo, daremos o nome proxy.rb ao arquivo.

Para nosso caso de uso, entender os passos acima é o suficiente. Porém, caso queira se aprofundar nos services do Rails, o link abaixo fornece um exemplo de implementação (bastante) diferente do que iremos utilizar, mas ainda interessante para estudo.

[Using Service Objects in Ruby on Rails | AppSignal Blog](https://blog.appsignal.com/2020/06/17/using-service-objects-in-ruby-on-rails.html)