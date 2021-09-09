# Utilização do Git em Projetos

Na Struct usamos o Git como ferramenta para gerenciamento de versões em todos os nossos projetos, usado o GitHub para armazenamento de todos.
Como membro da Struct, você deve passar seu usuário do GitHub para a diretoria da empresa quando for solicitado durante sua efetivação. Após isso você será adicionado ao time da Struct no site e terá acesso aos repositórios da empresa.

Como membro da empresa será esperado que você siga alguns padrões e boas práticas durante seu uso do Github, a fim de garantir a organização dos nossos repositórios.

## Branches
Quando você for designado à uma Issue em um projeto, a primeira coisa que você deve fazer é criar uma *branch* do código para trabalhar. Nessa etapa, lembre-se sempre de criar a branch a partir da main/master e de, antes de criá-la, dar `git pull` no código, para garantir que você está trabalhando na versão mais atualizada do código.

### Nome da Branch
Na Struct seguimos um padrão de nome para dar para a *branch*. A primeira coisa a saber é qual o número da sua Issue no Github (você pode ver isso ao lado do nome dela na página da Issue). 
Com isso em mãos, começamos o nome da *branch* com o seu número (com três dígitos) e escrevemos resumidamente o propósito da Issue, separando tudo por `_`.

Como exemplo, se estamos trabalhando na Issue de número #28 para criação de uma página de login, um possível nome para nossa *branch* seria `028_pagina_login`. 

## Commits
### Faça commits frequentes
Ao trabalhar em uma *issue* durante um projeto, evite fazer todo o trabalho em só um *commit*. Divida a funcionalidade a serem realizadas em partes, e faça um *commit* para cada uma das partes.

Por exemplo, se você está trabalhando em uma *issue* de criação de uma página de login completa, poderíamos dividir a tarefa nas seguintes etapas (cada uma representando um *commit*):
|  | Descrição da Tarefa |
|--|--|
| **Tarefa 1** | Criar base da página no HTML (Inserir *headers*, textos, campos e imagens) |
| **Tarefa 2** | Estilizar página (CSS) |
| **Tarefa 3** | Adicionar animações |
| **Tarefa 4** | Integrar com a API |

{% hint style="info" %}
Algumas *issues* menores, como de correção de bugs, podem ser feitas com apenas um *commit*. Organize suas tarefas antes de começar para prever quantos *commits* serão necessários.
{% endhint %}

### Descreva seus commits com *emojis*
O Github permite que *emojis* sejam incluídos nas descrições dos *commits* usando atalhos. Os *emojis* devem ser a primeira coisa adicionada a descrição do *commit* e indica que tipo de tarefa foi realizada nele. Alguns exemplos mais usados de emojis, seus atalhos e significados podem ser vistos abaixo:
| Emoji | Atalho | Significado |
|--|--|--|
| 🐛 | `:bug:` | Correção de um bug |
| :sparkles: | `:sparkles:` | Nova funcionalidade |
| :lipstick: | `:lipstick:` | Atualização na UI e nos arquivos de estilização |
| :white_check_mark: | `:white_check_mark:` | Adição, atualização ou passagem de testes |
| :twisted_rightwards_arrows: | `:twisted_rightwards_arrows:` | Merge de branches |
| :iphone: | `:iphone:` | Responsividade de páginas |
| :zap: | `:zap:` | Melhoria na performance do código |

Para a lista completa de *emojis* que podem ser usados nos *commits*, use o site [gitmoji](https://gitmoji.dev/).

### Descreva seus commits de forma clara e concisa
Na Struct nós usamos a descrição dos *commits* apenas para identificar o que foi feito, sem necessidade de descrever como foi feito nem dar maiores detalhes (isso fica nos Pull Requests). 
Com isso em mente, sempre escreva descrições curtas e bem descritivas do que foi feito.

❌ O que não fazer:  
> correcoes feitas
> Aprimorado UI da página de login usando padrão definido no figma e react-responsive-caroussel no carrossel

✅ O que fazer: 
> 🐛 Imagens não aparecendo no login corrigido
> :lipstick: Estilização da página de login

{% hint style="info" %}
Dica: use o comando `git commit -m "<Descrição aqui>"` para dar o *commit* e escrever a mensagem em apenas uma linha. 
{% endhint %}

## Pull Requests (PRs)
### Teste seu código
Embora pareça ser algo básico, muitas pessoas não testam seu código por completo antes de realizar um *Pull Request*. Ao fim da Issue, tente testar tudo que você programou, e, caso tenha modificado algum código usado por outras partes do projeto (um método ou um componente por exemplo), verifique as partes do programa, tanto no back quanto no front, que usam ele, e garanta que elas não tenham sido quebradas pelas suas modificações.

#### RSpec
No caso de você estar fazendo uma Issue do Backend, caso tenha sido criado ou modificado models ou controllers, lembre-se se criar ou atualizar os testes em RSpec de tudo que for feito por você na Issue.

Além disso, rode todos os testes de RSpec criados, a fim de verificar se seu código continua passando em todos.

#### Rubocop
Em casos de se estar trabalhando no Backend da aplicação, execute também o *rubocop* ao final de sua programação, a fim de conferir se seu código segue bons padrões de escrita. 

### Criando o Pull Request 
Com tudo no seu código feito e testado, seguindo o que foi pedido na sua Issue, só falta você criar seu Pull Request no Github.  Dê um `git push` na sua *branch* e já deve aparecer na página principal do projeto a opção de criar o PR.

#### Nome do PR 
Por padrão, o Github irá colocar como nome do *Pull Request* o nome da sua *branch* ou o nome do commit feito (caso só haja um commit).
Embora não exigimos que os membros da Struct troquem esse nome na criação do PR, é recomendado que coloque um nome mais descritivo, se o nome automático já não estiver.

#### Descrição do PR
Esse é o momento de dar maiores detalhes sobre o que você fez e como foi feito, contendo as seguintes informações:

##### O que foi feito
Comece listando tudo o que foi feito na sua *branch*, tanto as coisas que já estavam definidas em sua Issue quanto outras coisas que você teve que modificar para deixar tudo funcional.
Use essa etapa para ir na seção do Github de arquivos modificados do *Pull Request* e revisar tudo o que foi feito, detalhando isso na descrição do PR.

##### Como foi feito
Aqui você descreverá como você executou o que foi detalhado na etapa anterior. Você corrigiu um bug? Detalhe o que estava causando ele e o que você fez para corrigir. Utilizou uma gem/componente externo? Detalhe qual foi e qual foi seu motivo de utilizá-lo. Tudo que você achar relevante de falar sobre o que foi feito em seu código é para estar aqui.

##### Como foi testado
Nessa etapa detalhe o que você fez para garantir que seu código estava funcionando. Em alguns casos, em especial no front, somente citar que todas as páginas modificadas foram acessadas e todas as possibilidades de ações do cliente nelas foram testadas já é o suficiente. Qualquer coisa a mais que você fizer para validar o funcionamento vale a pena ser citado aqui.
Para o Back, informe sobre os testes *RSpec* criados e testados, e também sobre quais outras formas você testou os métodos criados (Insomnia, Rails Console...). Novamente, qualquer coisa diferente usada para testagem detalhe aqui também.

##### Responsividade
Para o caso de Issues no front, detalhe também sobre como sua implementação está funcionando em diferentes tamanhos de telas, sendo os mais importantes os seguintes:

- Smartphone
- Tablet
- 1024
- 1280
- 1440
- 1920

##### Template
Para evitar esquecer qualquer coisa na hora de descrever seu *Pull Request*, siga o template a seguir:

```
# O que você fez?
<Descrição do que foi feito no PR>

# Como você fez?
<Detalhes sobre como foi a implementação do que foi descrito no item anterior>		

# Para cada tópico qual foi a forma de teste?
<Detalhes sobre como foi testado seu código>

<!-- Para o Caso de Frontend, caso não tenha apague-->

# Responsividade
<!-- Para cada tamanho de tela testado, coloque :thumbsup: caso tenha funcionado e  :thumbsdown: para caso não funcione AINDA! Caso a MR seja de backend, apague esse tópico-->
- :thumbsup:/:thumbsdown: Smartphone - <Detalhe sobre o que não está funcionando, no caso negativo>
- :thumbsup:/:thumbsdown: Tablet - <Detalhe sobre o que não está funcionando, no caso negativo>
- :thumbsup:/:thumbsdown: 1024 - <Detalhe sobre o que não está funcionando, no caso negativo>
- :thumbsup:/:thumbsdown: 1280 - <Detalhe sobre o que não está funcionando, no caso negativo>
- :thumbsup:/:thumbsdown: 1440 - <Detalhe sobre o que não está funcionando, no caso negativo>
- :thumbsup:/:thumbsdown: 1920 - <Detalhe sobre o que não está funcionando, no caso negativo>
```
