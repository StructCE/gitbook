# Cloudinary
 
O Cloudinary é uma ferramenta para armazenamento de imagens, vídeos e outros arquivos online. Nele é possível integrar com o Active Storage para fazer upload de arquivos tanto estaticamente (pelo seed) quanto dinamicamente (funções no back-end de adicionar imagens).
 
## Como usar o Cloudinary
 
O passo a passo para usar o Cloudinary é o seguinte:
 
- Criar conta no Cloudinary
- Instalar a gem Cloudinary
- Configurar as credenciais por meio de um dos métodos possíveis.
- Configurar para que o Cloudinary seja o padrão para o active storage
 
### Criar conta
 
Esse passo é bem simples, é como criar conta em qualquer outro site. Você deve colocar um nome, um email e uma senha, indicar seu país, colocar o nome de sua empresa ou site se quiser e selecionar um dos 3 produtos que o site oferece.
 
Nesse caso, escolhemos a opção: Programmable Media for image and video API.
 
Dessa forma, se você colocar um nome para a empresa ou site, o Cloud Name será esse mesmo nome em letras minúsculas e sem espaços. Se você omitir essa informação, o Cloud Name será um conjunto aleatório de letras.
 
Para usar sua conta você terá que verificar seu email.

### Instalar a gem Cloudinary

Para instalar a gem, é como instalar todas as outras gems, é só adicionar essa linha no gemfile:
```ruby
gem 'cloudinary'
```
E rodar bundle para instalar a gem.

### Credenciais

Para essa parte, existem múltiplas maneiras de integrar as suas credenciais com o Cloudinary. 

Uma delas é adicionar um arquivo chamado *cloudinary.rb* dentro da pasta */config/initializers* com o seguinte contéudo:

```ruby
Cloudinary.config do |config|
    config.cloud_name = 'sample'
    config.api_key = '874837483274837'
    config.api_secret = 'a676b67565c6767a6767d6767f676fe1'
    config.secure = true
end
```
Dessa forma, substitua o *'sample'* em *config.cloud_name* pelo nome da empresa (ou o conjunto aleatório de letras conforme visto na parte de criar a conta), o que está em *config.api_key* pela sua api_key (fornecida quando se entra na conta) e o que está em *config.api_secret* pela sua api_secret (também fornecida quando se entra na conta).

Para mais informações, acesse o [site da Cloudinary](https://cloudinary.com/documentation/rails_integration#configuration).

### Configuração para Active Storage

Para configurar o Cloudinary para ser o padrão em requisições do Active Storage, basta colocar um arquivo chamado *storage.yml* dentro da pasta *config* com o seguinte conteúdo:
```yml
cloudinary:      
  service: Cloudinary
  # Any other settings you want, to be sent on all requests, can be included here as well.
```

E adicionar a seguinte linha no arquivo config/environments/development.rb(para o development - se quiser para production, coloque no arquivo config/environments/production.rb):

```ruby
# Use Cloudinary.
config.active_storage.service = :cloudinary
```

Para mais informações sobre como fazer uploads diretos, acesse [esse site da Cloudinary sobre o Active Storage](https://cloudinary.com/documentation/rails_activestorage).


E pronto, o Cloudinary deve estar funcionando corretamente agora.