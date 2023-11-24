# Fazendo o deploy de um react-app padrão

Considerando que nenhum framework, e nem SSR, está sendo usado, o app react não inclui servidor. No ambiente de desenvolvimento são usadas ferramentas para servir o app na porta determinada (na Struct determinamos como 3000), mas no deploy que ferramenta é usada? O NGinx.

## Configurando o repositório

Considere a [branch production do projeto front-end-template](https://github.com/StructCE/react-template/tree/production) e [suas alterações](https://github.com/StructCE/react-template/compare/main...production).

### Configurando o NGinx

O NGinx é um servidor web que pode ser usado para servir arquivos estáticos, como imagens, css, js, etc. Sendo assim, depois que nosso app react é buildado, ele é servido pelo NGinx.

Para isso, é necessário criar um arquivo de configuração para o NGinx na raíz do projeto, chamado `nginx.conf`. Esse arquivo deve conter:

```nginx
server {
  listen 80 default_server;
  listen [::]:80 default_server;
  root /usr/share/nginx/html;
  server_name dominio.exemplo.ex www.dominio.exemplo2;
  location / {
    root /usr/share/nginx/html;
    index index.html index.htm;
    try_files $uri $uri/ /index.html =404;
  }
}
```

Trocando os valores de `dominio.exemplo.ex` e `www.dominio.exemplo2` pelos domínios que o app será servido. Por exemplo, se o app for servido em `www.struct.com.br`, o arquivo deve conter:

```nginx
server {
  listen 80 default_server;
  listen [::]:80 default_server;
  root /usr/share/nginx/html;
  server_name www.struct.com.br;
  location / {
    root /usr/share/nginx/html;
    index index.html index.htm;
    try_files $uri $uri/ /index.html =404;
  }
}
```

### Mudando as urls de localhost

O app react usa urls locais para acessar a API, por exemplo, `http://localhost:3333/api/v1`. Essas urls devem ser alteradas para as urls de produção, por exemplo, `https://api.struct.com.br/api/v1`.

É possível fazer isso usando variáveis de ambiente, mas no momento deve ser trocado manualmente, como no nosso repositório de exemplo (talvez esse gitbook esteja desatualizado em relação ao repositório, verifique).


### Mudando o index.html

O arquivo `index.html` deve ser alterado para conter informações corretas sobre o app, e metadados. Talvez também seja útil criar um `robots.txt`, que serve para ajudar mecanismos de busca a indexar o site da maneira desejada, veja de acordo com seu projeto.

As mudanças gerais são colocar o título correto, colocar descrição, mudar o favicon e a linguagem para pt-BR.


## Configurando o servidor

### Criando a docker image

Vá para a branch production localmente. Crie um arquivo chamado `Dockerfile` na raíz do projeto. Use como base os templates de projetos recentes anteriores, e atualize o url do git presente no arquivo, mudando o nome do projeto e o token de oauth do github ([veja aqui](./README.md#crie-a-imagem-docker)).

### Criando o container

Dê um git pull no repositório de docker_compose da Struct, e crie uma pasta com o nome do projeto. Modifique o template de docker-compose do Traefik com os nomes que podem ser usados para identificar o projeto nos logs, caso ocorra algum erro.

Além da configuração do traefik, é importante definir a imagem que será usada com o valor de `image`, alterar os valores de `environment`, `restart`, `volumes`, e `networks`. Use um projeto anterior como base.

Crie o container usando o comando `docker-compose up -d`. A imagem será baixada do repositório da Struct, e o container será criado e rodado em plano de fundo.
