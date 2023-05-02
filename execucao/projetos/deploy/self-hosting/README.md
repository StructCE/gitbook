{% hint style="warning" %} 
Leia antes para entender o que é [imagem e container docker](/execucao/projetos/docker/README.md).
{% endhint %}

# Nosso servidor

No momento, pagamos por um servidor no DigitalOcean, que é um serviço de cloud computing, ou seja, uma plataforma que usa a conectividade da internet para hospedar e prover recursos, programas e informações em nuvem, e usamos ssh para acessá-lo e fazê-lo rodar exatamente o que queremos.


## Nossa infraestrutura

Usamos Docker e Docker Compose para poder isolar e rodar vários servidores na mesma máquina. Para levar o tráfego que chega em nossa máquina para o container correto, usamos o [Traefik v2](https://doc.traefik.io/traefik/) como [proxy reverso](https://pt.wikipedia.org/wiki/Proxy_reverso).

É mantido um repositório no gitbucket com os Dockerfiles utilizados para construir as imagens do nosso servidor.

É mantido um repositório que está presente no servidor, com os arquivos do Docker Compose utilizados para rodar as imagens construídas.

## Fazendo deploy

### Configure o projeto

Crie uma branch `production`, caso não exista, no projeto desenvolvido, e faça a configuração específica para esse deploy.

{% hint style="warning" %} 
Também adicione `Dockerfile` ao `.gitignore` do projeto.
{% endhint %}

### Crie a imagem docker

{% hint style="danger" %}
Não coloque Dockerfiles no repositório do projeto, utilize o repositório do gitbucket para isso.

Colocar esse arquivo no projeto pode causar problemas de segurança, e não é uma boa prática. Muitos dos nossos Dockerfiles usam credenciais que não devem ser expostas.
{% endhint %}

Pegue o template de `Dockerfile` (no momento não existe template, então busque do último projeto produzido) e modifique conforme necessário para gerar uma imagem docker.

Para gerar a imagem, use o comando `docker build -t structej/projetos:nome-projeto-1.0 .` na raíz do projeto. Isso constrói a imagem e coloca a tag `nome-projeto-1.0` nela.


Várias das nossas imagens são um pull do projeto, e para isso é necessário um token de acesso no github. Para gerar esse token, pode ser seguida a [documentação do github](https://docs.github.com/pt/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token#creating-a-personal-access-token-classic).


### Faça o push da imagem

Faça login no Docker Hub, usando o comando `docker login`. Talvez seja necessário inserir as nossas credenciais.

Faça o push da imagem para o Docker Hub, usando o comando `docker push structej/projetos:nome-projeto-1.0`. Isso envia a imagem para o Docker Hub, onde ela pode ser acessada pelo docker-compose.

{% hint style="info" %}
O `structej/projetos` é o `usuário/projeto` que enviamos a imagem de tag `nome-projeto-1.0`. É importante fazer assim, pois por padrão projetos no Docker Hub são públicas, então enviamos ela para um repositório que sabemos ser privado.
{% endhint %}

### Faça o docker-compose no servidor

{% hint style="info" %} 
Estamos guardando templates de docker-compose.yml na pasta `templates` do repositório presente no servidor. Veja atualizações por lá.
{% endhint %}

{% hint style="info" %} 
É recomendado fazer as atualizações localmente, dar um push para o repositório, e depois dar um pull no servidor.
{% endhint %}

Faça o pull/clone do repositório do Docker Compose, usando o comando `git pull/clone`. Crie um docker-compose.yml com o serviço do projeto, usando o template de `docker-compose.yml` (no momento o template só inclui configuração do traefik, então busque configurações adicionais do último projeto produzido).

O template de traefik possui palavras chaves que devem ser substituídas. Utilize múltiplos cursores para garantir que não esqueceu de alterar uma das palavras chaves em algum lugar.

## Atualizando o deploy

### Atualize a branch `production`

Peça para que um membro da equipe faça um PR para a branch `production` do projeto, com as adições que devem ser feitas no deploy.

Procure por coisas que podem quebrar ou requerem passos adicionais no deploy, como mudanças de banco de dados, ou mudanças de configuração de serviços.

### Atualize a imagem docker

Faça o build da imagem docker, usando o comando `docker build -t structej/projetos:nome-projeto-x.x .` na raíz do projeto.

Agora a versão da imagem docker é `x.x`. Sempre incrementamos a versão da imagem docker, para que possamos fazer o rollback caso algo aconteça de errado.

Faça o push da imagem para o Docker Hub, usando o comando `docker push structej/projetos:nome-projeto-x.x`.

{% hint style="danger" %}
O que pode acontecer de errado?
- A branch possuía coisas que quebram o deploy, e o container fica em estado de erro. Nesse caso, o traefik não consegue acessar o container, e o site fica fora do ar;
- A atualização à branch introduziu um bug grave, mas o container não fica em estado de erro. Nesse caso, o traefik consegue acessar o container, mas o site pode não funcionar corretamente;
- O Dockerfile foi alterado e possui alguma coisa errada (por exemplo em versionamento), mas o build ainda funciona. Nesse caso, novamente, o traefik consegue acessar o container, mas o site pode não funcionar corretamente;
- etc.
{% endhint %}

### Atualize o docker-compose no servidor

Mude a propriedade `image` do serviço do projeto no docker-compose.yml para a versão atual da imagem docker. Faça o commit e o push do docker-compose.yml.

Exemplo:
```docker-compose
version: '3.7'

services:
    service-we-want-to-update:
        image: structej/projetos:nome-projeto-x.x
        ...
```

