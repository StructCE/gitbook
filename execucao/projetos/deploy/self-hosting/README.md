{% hint style="warning" %} 
Leia antes para entender o que é [imagem e container docker](/execucao/projetos/docker/README.md).
{% endhint %}

# Nosso servidor

No momento, pagamos por um servidor no DigitalOcean, que é um serviço de cloud computing, e usamos ssh para acessá-lo.


## Nossa infraestrutura

Usamos Docker e Docker Compose para poder isolar e rodar vários servidores na mesma máquina. Para levar o tráfego que chega em nossa máquina para o container correto, usamos o Traefik v2 como proxy reverso.

É mantido um repositório no gitbucket com os Dockerfiles utilizados para construir as imagens do nosso servidor.

É mantido um repositório que está presente no servidor, com os arquivos do Docker Compose.

## Fazendo deploy

### Configure o projeto

Crie uma branch `production`, caso não exista, no projeto desenvolvido, e faça a configuração específica para esse deploy.

### Crie a imagem docker

Pegue o template de `Dockerfile` (no momento não existe template, então busque do último projeto produzido) e modifique conforme necessário para gerar uma imagem docker.

Para gerar a imagem, use o comando `docker build -t structej/projetos:nome-projeto-1.0 .` na raíz do projeto.

Várias das nossas imagens são um pull do projeto, e para isso é necessário um token de acesso no github. Para gerar esse token, pode ser seguida a [documentação do github](https://docs.github.com/pt/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token#creating-a-personal-access-token-classic).


### Faça o push da imagem

Faça login no Docker Hub, usando o comando `docker login`. Talvez seja necessário inserir as nossas credenciais.

Faça o push da imagem para o Docker Hub, usando o comando `docker push structej/projetos:nome-projeto-1.0`.

### Faça o docker-compose no servidor

{% hint style="info" %} 
Estamos guardando templates de docker-compose.yml na pasta `templates` do repositório dos docker-compose. Veja atualizações por lá.
{% endhint %}

Faça o pull/clone do repositório do Docker Compose, usando o comando `git pull/clone`. Crie um docker-compose.yml com o serviço do projeto, usando o template de `docker-compose.yml` (no momento o template só inclui configuração do traefik, então busque configurações adicionais do último projeto produzido).

## Atualizando o deploy

### Atualize a branch `production`

Peça para que um membro da equipe faça um PR para a branch `production` do projeto, com as adições que devem ser feitas no deploy.

Procure por coisas que podem quebrar ou requerem passos adicionais no deploy, como mudanças de banco de dados, ou mudanças de configuração de serviços.

### Atualize a imagem docker

Faça o build da imagem docker, usando o comando `docker build -t structej/projetos:nome-projeto-x.x .` na raíz do projeto.

Agora a versão da imagem docker é `x.x`. Sempre incrementamos a versão da imagem docker, para que possamos fazer o rollback caso dê merda.

Faça o push da imagem para o Docker Hub, usando o comando `docker push structej/projetos:nome-projeto-x.x`.

### Atualize o docker-compose no servidor

Mude a propriedade `image` do serviço do projeto no docker-compose.yml para a versão atual da imagem docker. Faça o commit e o push do docker-compose.yml.

```docker-compose
version: '3.7'

services:
    service-we-want-to-update:
        image: structej/projetos:nome-projeto-x.x
        ...
```

