# Sprints

Uma *sprint* consiste em um conjunto de features do projeto que deve ser desenvolvido em um conjunto específico de tempo. Cada feature possui atrelada a ela uma pontuação e um membro responsável pelo seu desenvolvimento. A utilização de *sprints* é uma característica do desenvolvimento ágil e possui o intuito de validar constantemente o projeto junto ao cliente por meio de entregas constantes de features \(as *sprints* também são úteis para impedir que os desenvolvedores percam os prazos do projeto\).

Como gerente de projetos, é seu trabalho definir todas as características de uma *sprint*, incluindo a sua duração, as features que serão desenvolvidas, a pontuação de cada feature e quem será responsável por cada feature. Também é seu trabalho gerenciar o andamento da *sprint*, garantindo que os desenvolvedores estejam desenvolvendo as features de forma adequada \(com a utilização correta de branches e com a implementação de testes e utilização de comentários\), esclarecendo quaisquer dúvidas relacionadas às regras de negócio do projeto, documentando o desenrolar da *sprint* quando ela acabar e redistribuindo features para outras *sprints* caso isso seja necessário.

No início de uma *sprint*, é altamente recomendado que, independente das circunstâncias, seja realizada **uma reunião com a equipe de desenvolvimento.** Isso permite ao gerente de projetos tratar todas as pendências necessárias relativas à *sprint* passada e ao começo de uma nova *sprint*.

Você também deverá criar um cartão no *Trello* (ou no kanbam no próprio github) no início da *sprint* para abrigar os detalhes da *sprint*. Esse cartão deverá ser atualizado no final da *sprint* ou caso alguma mudança ocorra nos detalhes da *sprint*.

Esta seção aborda como features devem ser elaboradas e integradas ao projeto, como o desenvolvimento de uma feature deve ser feito por um membro da equipe e quais as práticas que devem ser adotadas ao final de uma *sprint*.

## Features

Como dissemos, uma feature é uma parte do projeto que fornece alguma funcionalidade, e o desenvolvimento do projeto será divido no desenvolvimento de várias features. As features a serem desenvolvidas devem ser derivadas dos requisitos do projeto, colhidos em reuniões com o cliente. Por fim, as features devem ser divididas de forma que possam ser desenvolvidas por um único membro do projeto \(ou seja, sem dependências *excessivas* com o código de outras features\).

Com o intuito de deixar o desenvolvimento do projeto organizado, cada feature deve ser registrada no repositório do projeto por meio de uma *issue*, onde todos os detalhes necessários para o desenvolvimento da feature devem estar presentes. Dessa forma, qualquer desenvolvedor que **não** conheça os requisitos do projeto consegue desenvolver a feature apenas lendo a descrição da *issue*. Aliás, qualquer membro do projeto deve abrir uma issue quando perceber que uma nova feature precisará ser desenvolvida ou quando notar algum bug no projeto que não possa ser resolvido trivialmente.

No início de uma *sprint*, o gerente de projeto escolhe quais features serão desenvolvidas nessa *sprint* a partir das *issues* contidas no repositório, priorizando as correções de bugs e as features demandadas pelo cliente do projeto. Caso não haja *issues* no repositório, o gerente deve se reunir com a equipe de desenvolvimento para registrar as features pendentes como *issues* ou notificar o diretor de projetos que é necessário colher mais requisitos com o cliente.

<!-- Após as features serem escolhidas, elas devem ser pontuadas pela equipe de desenvolvimento. A forma de pontuar uma feature é bem simples: o gerente se reúne com a equipe de desenvolvimento, descreve o trabalho envolvido nessa feature e pede que a equipe de desenvolvimento indique um número entre os 6 primeiros números da sequência de Fibonacci \(1, 2, 3, 5, 8, 13\) que descreva quão trabalhosa a feature seria para ser desenvolvida \(incluindo testes e comentários\). Caso os desenvolvedores concordem \(em linhas gerais\) na pontuação, ela é atribuída à feature; do contrário, os desenvolvedores conversam entre si para se chegar a um consenso. Caso a feature tenha uma pontuação maior ou igual a 5, ela é denominada um *épico*, e deve ser dividida em sub-features menores. É importante frisar que **correções de bugs não valem pontos**. -->

Após as features serem escolhidas, elas devem ser discutidas com os membros da equipe de desenvolvimento e, em seguida, distribuídas entre eles. É importante garantir que a distribuição seja bem feita e leve em consideração a grade horária semanal dos desenvolvedores para evitar membros ociosos ou membros atarefados excessivamente. Também é ideal que desenvolvedores novatos sejam auxiliados no desenvolvimento de features mais complexas, por meio de recursos como *pair programming* ou maior atenção do gerente de projetos. Por fim, lembre-se de atribuir as *issues* no repositório aos seus respectivos responsáveis para que qualquer um que visite o repositório do projeto possa saber quem está trabalhando no que.

Assim que as features forem escolhidas, discutidas e distribuídas, é hora de começar o desenvolvimento.

## Desenvolvimento

O desenvolvimento de uma feature em uma *sprint* deve seguir uma lógica bem definida para garantir que as diversas features desenvolvidas venham a ser adequadamente revisadas e integradas no projeto. Como gerente de projetos, você deverá entender plenamente essa lógica e explicá-la aos demais desenvolvedores.

Como dito anteriormente, seu projeto deve ter três branches principais: *develop*, *main* e *production*. O primeiro passo a ser feito no começo de cada *sprint*, é atualizar a branch *develop* com as mudanças contidas na branch *main*.

Depois disso, para **cada feature** a ser desenvolvida, os seguintes passos devem ser executados:

  1. O desenvolvedor deve abrir uma nova branch **a partir da develop**, com o padrão de nomenclatura `numero_da_issue_nome_da_feature` \(Exemplo: 001_tela_de_login\).

  2. O desenvolvedor deve, nessa nova branch, desenvolver sua feature, **com testes e comentários.** Após o desenvolvimento acabar, o desenvolvedor deve abrir uma *pull request* da sua branch para a branch *develop*, **resolvendo qualquer conflito** com a branch *develop* após abir a *pull request*.

  3. Um outro desenvolvedor \(que não seja o que desenvolveu a feature\) deve **revisar** essa *pull request*, rodando e inspecionando os testes e verificando quais foram as mudanças realizadas, se há bugs no código, se a feature está de acordo com as regras de negócio do projeto e se mais testes precisam ser redigidos. Esse passo é **extremamente importante** para garantir que o código do projeto possua alta qualidade e seja livre de bugs.

  4. Caso a revisão seja bem sucedida, o revisor resolve qualquer conflito que tenha surgido entre a submissão da *pull request* e a sua revisão, e aceita a *pull request*. Do contrário, o revisor notifica nos comentários da *pull request* as mudanças que o desenvolvedor deve adotar para que a *pull request* seja aceita e voltamos ao passo 2.

Esses passos devem ser executados até que a *sprint* chegue ao fim, o que ocorre quando todas as features da *sprint* foram desenvolvidas **ou** quando a data de finalização da *sprint* é atingida.

## Finalização

Quando uma *sprint* chega ao fim, os seguintes passos devem ser executados para preparar o projeto para a próxima *sprint*:

  1. Todas as *pull requests* que estejam abertas devem ser resolvidas. Isso pode ser feito com a *pull request* sendo aceita ou com a *pull request* sendo recusada e a feature relativa a ela sendo postergada para a próxima *sprint*.

  2. Uma *pull request* deve ser aberta da branch *develop* para a branch *main*. Essa *merge request* deve ser revisada por **todos** os membros da equipe de desenvolvimento. Essa revisão é mais sucinta que as outras revisões e tem o intuito de verificar se as features desenvolvidas foram integradas de maneira correta, se os testes estão sendo bem sucedidos ao serem executados e se a aplicação roda adequadamente \(isso deve ser testado por um breve uso da aplicação em si\).

  3. Caso todos os membros aprovem a *pull request* da *sprint*, as features desenvolvidas na *sprint* são colocadas na branch *main*. Do contrário, as mudanças necessárias ou são implementadas rapidamente ou, caso se tratem de mudanças mais sérias, são colocadas em novas *issues* que serão resolvidas na próxima *sprint*. Nesse caso, a *pull request* poderá ser aceita para a *main* caso os bugs e problemas sejam poucos \(mesmo com alguns problemas, é bom que o código seja colocado na main para evitar que features prontas se acumulem na develop\). As correções de bugs e reparo de features incompletas **devem ter prioridade** na próxima *sprint*.

  4. Caso a *pull request* tenha sido aprovada sem bugs ou ressalvas, as mudanças colocadas na *main* devem ser colocadas também na branch *production*, para que o cliente tenha acesso as mudanças. Caso a branch *production* esteja muito atrasada em relação a branch *main*, considere realizar uma *sprint* apenas com o intuito de corrigir bugs.

Como gerente de projetos, você também deverá fazer,ao final da seamana, um breve resumo da *sprint*, relatando o resultado final da *sprint*, as features desenvolvidas por cada membro da equipe e as dificuldades encontradas, além de falar sobre a situação geral do projeto. Esse resumo deverá ser mandado no canal de **gerência de projetos no *slack*** direcionado ao diretor de projetos, para que ele possa estar inteirado da situação do projeto.
