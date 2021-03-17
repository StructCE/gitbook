# Mailer

Mailer é um framework responsável pelos serviços de entrega e recebimento de e-mails.

## Mailjet

Mailjet é mailer global que ajuda a enviar e a rastrear a entrega de e-mails através de sua API, além de ser útil para serviços de autenticação e para gerenciar subcontas e contatos.

### Uso

No Rails, é possível acessar as funcionalidades desse mailer através da gem *mailjet*, mas para tal, será necessário ter um conta [em seu site](https://www.mailjet.com/) para obter a chave para a API. Em seguida, será preciso adicionar a chave a um inicializador na seguinte forma:

Rode o comando `$ rails generate mailjet:initializer` para gerar o arquivo, o comando deve solicitar sua chave da API, sua chave secreta e o e-mail ligado à sua conta da mailjet.

Por fim, para utilizar o Mailjet, é necessário adicionar o seguinte trecho ao arquivo em que está sendo utilizado:  
```
require 'mailjet'
Mailjet.configure do |config|
  config.api_key = ENV['MJ_APIKEY_PUBLIC']
  config.secret_key = ENV['MJ_APIKEY_PRIVATE']  
  config.api_version = "v3.1"
end
```

#### Exemplos

Criando um novo contato:
```
variable = Mailjet::Contact.create(email: "Mister@mailjet.com")
p variable.attributes['Data']
```

Para acessar todos os objetos: `recipients = Mailjet::Listrecipient.all(limit: 0)`

Acessando objeto específico:  
```
variable = Mailjet::Contact.find($CONTACT_EMAIL)
p variable.attributes['Data']
```

Atualizando propriedades de um objeto: `variable.update_attributes(html_part: "Hello <strong>world</strong>!",text_part: "Hello world!")`

#### Enviando emails com ActionMailer

No arquivo <i>application.rb</i> adicione a linha `config.action_mailer.delivery_method = :mailjet`

Para enviar e-mails através da API é preciso criar um novo recurso *MessageDelivery*:
`Mailjet::MessageDelivery.create(from: "meu@exemplo.com", to: "seu@exemplo.com", subject: "Funcionamento do Mailjet", text: "Sua mensagem aqui.")`

Também é possível enviar para múltiplos destinatários de uma vez passando um array de e-mails ao invés de apenas um. (`to: ["email1@exemplo.com", "email2@exemplo.com"]`)

Para mais informações acesse o [Repositório do Mailjet](https://github.com/mailjet/mailjet-gem).
