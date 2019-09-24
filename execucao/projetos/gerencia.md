# Gerência de projetos

O gerente de um projeto possui funções essenciais à qualidade de vida de um projeto, como a criação do projeto em si, a gerência das sprints do projeto e a comunicação dos detalhes do projeto para os outros membros de equipe nas reuniões gerais. Em suma, o gerente do projeto conduz a execução do projeto, tomando as medidas necessárias para que seu desenvolvimento seja bem sucedido.

Está pagina contém as informações necessárias para se gerenciar um projeto de maneira adequada.

## Início do projeto

O primeiro passo em um projeto de software consiste na criação e configuração do repositório em que o projeto será desenvolvido. Isso inclui criar o repositório do projeto, as estruturas de pastas para abrigar o código fonte e outros recursos e configurar adequadamente os arquivos de controle de versão, os arquivos de documentação do projeto, a utilização de bibliotecas externas \(gems\), o banco de dados do projeto e a geração de imagem do projeto \(docker\).

Embora isso pareça ser muita coisa, iremos detalhar melhor cada passo nas seções abaixo.

### Projeto Rails

O primeiro passo na inicialização do projeto é a criação do projeto na framework [*Ruby on Rails*](../ruby-on-rails/README.md). Para isso, vamos escolher, utilizando o RVM ou Rbenv, uma versão de Ruby esteja um *minor release* atrás da última versão \(ou seja, se a última versão de Ruby é a 2.x, utilize a versão 2.x-1 para o projeto\). Na dúvida, utilize a versão de Ruby utilizada no último projeto. Isso evita que tenhamos que lidar com os bugs inerentes à versão mais nova do Ruby e das gems que o acompanham. Caso algum dos membros do projeto não tenha um gerenciador de versão de Ruby instalado \(como RVM e Rbenv\), ajude ele com a instalação \(esse tipo de software é praticamente essecial para se trabalhar em vários projetos, cada um com uma versão diferente de Ruby\).

Após escolher a versão de Ruby desejada e instalar em seu computador a gem *rails*, rode o comando `rails new nome_do_projeto_em_snake_case`. O framework cuidará da criação de pastas e arquivos para o desenvolvimento do projeto.

Lembre-se de verificar qualquer mensagem de erro ou aviso de *deprecated gem* gerado pelo Rails. Se possível, corrija estes problemas **antes** de seguir para o próximo passo.

Por fim, adicione todos os arquivos gerados ao controle de versão sob o nome 'Commit inicial'.

### Repositório

A criação do repositório para o projeto deve ser feita no grupo da Struct do GitLab. O nome do repositório geralmente segue o padrão `projeto_nome` ou `projeto_codinome` \(como gerente de projeto, sinta-se livre para criar um codinome épico para o projeto :grinning:\). Configure o repositório como privado e **não** inicialize ele com um README, pois o Rails já gerá esse arquivo para você. Após criar o repositório, faça o upload dos arquivos gerados pelo projeto de Rails para o repositório.

### Segundo commit

#### README

#### Arquivos padrão

#### Configuração de gems

### Criação de branches padrão

### Banco de dados

### Docker

## Sprints

### Issues

### Desenvolvimento

### Finalização

## Reuniões gerais
