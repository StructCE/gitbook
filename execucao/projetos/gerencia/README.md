# Gerência de projetos

O gerente de um projeto possui funções essenciais à qualidade de vida de um projeto, como a criação do projeto em si, a gerência das *sprints* do projeto e a comunicação dos detalhes do projeto para os outros membros de equipe nas reuniões gerais. Em suma, o gerente do projeto conduz a execução do projeto, tomando as medidas necessárias para que seu desenvolvimento seja bem sucedido.

Está pagina contém as informações necessárias para se gerenciar um projeto de maneira adequada.

## Reuniões gerais

O gerente de um projeto também tem o trabalho de participar das reuniões gerais \(RGs\) da Struct para informar aos outros membros da empresa júnior \(em especial, o presidente e o diretor de projetos\) o estado de desenvolvimento do projeto. Nessa hora, o gerente deve destacar de forma bem resumida se o desenvolvimento do projeto está progredindo de maneira adequada, se há necessidade de mais pessoas serem alocadas no projeto e se algo de anormal está acontecendo com o projeto.

Caso o gerente de um projeto não possa comparecer à reunião geral, ele deve instruir algum outro membro do projeto que estará na RG à realizar essa função. Caso isso não seja possível, o gerente deve enviar uma mensagem breve no *Slack* que detalhe esses fatores.


## Soft Skills

Ser gerente não é só sobre ter capacitade técnica para pode revisar o que está sendo entregue e passar os devidos feedbacks ou sobre saber mostrar aos membros como desenvolver determinada funcionalidade, aliás, essas coisas não são tão relevantes para definir se um gerente está apto a assumir o cargo. As principais competências que um gerente precisa dominar são mais relacionadas a soft skills. Sendo assim, nessa seção, serão apresentadas alguns pontos para os futuros gerentes levarem em consideração longo do desenvolvimento do projeto.

### Sempre considere que irão ocorrer atrasos

Muitas vezes o projeto já chega em você com um prazo bem definido e você se vê tendo que criar um cronograma para tentar entregar todas as funcionalidades dentro do prazo estipulado. Mas lembre-se: **os pilotos não são máquinas**. Sempre ao longo do desenvolvimento de um projeto, todos os membros irão atrasar issues em algum momento, principalmente dada a natureza de uma EJ, em que os pilotos também estão ocupados com tarefas da universidade. 

Sendo assim, o seu objetivo é tentar minimizar ao máximo esses atrasos e o impacto que eles trazem para o desenvolvimento do projeto como um todo. Para isso, tente sempre montar o cronograma o mais realista possível (ou até bem pessimista), considerando que praticamente toda semana haverão issues em atraso. Além disso, para casos de atrasos recorrentes, é muito importante deixar sempre claro para os desenvolvedores o impacto desses atrasos para o progresso do projeto e para a relação com o cliente.

{% hint style="info" %}
    Procure sempre saber o motivo dos atrasos e evite passar a sensação para o membro de que "Atrasou, mas não tem problema", pois isso pode gerar uma sensação para a equipe como um todo de que não tem problema atrasar as atividades. Tente ajudar o membro que atrasou a correr atrás do que falta antes da próxima reunião.
{% endhint %}

### Organização

- Mantenha o controle de tudo que falta e do que já está feito;
- Se uma issue for mergeada sem estar 100%, anote o que ficou faltando ou crie uma nova issue;

### Relação com o cliente

#### Não deixe o cliente no escuro

Esse tópico entra um pouco no tópico anterior. Em um cenário nada ideal, existe a possibilidade de você como gerente se deparar com uma situação bem chata: não será possível entregar o projeto dentro do prazo. 

Mas o que devemos fazer agora? Tentamos correr atrás e fazer um milhão de coding days seguidos para tentar colocar o projeto de volta nos trilhos? Adicionamos mais membros ao projeto? Paramos a empresa inteira para fazer um mutirão para entregarmos o projeto? Bem, já adianto que, na maioria dos casos, essas possibilidades não irão funcionar, inclusive podem ter o efeito reverso e acabar atrasando o projeto ainda mais, visto que vão acabar desgastando os desenvolvedores.

Sendo assim, antes de sair procurando soluções para tentar cumprir com um prazo irreal, procure sempre entrar em contato com o cliente, explicando desde cedo os problemas que vocês estão enfrentando e já prepará-lo para um possível atraso, podendo até chegar a um acordo para realizar uma entrega inicial parcial, mesmo com algumas funcionalidades faltando.

{% hint style="warning" %}
    Ao falar sobre atrasos com o cliente, tente focar mais nas questões técnicas que causaram o atraso e evite dizer coisas como "está atrasando pois estamos em final de semestre na universidade", dando a impressão que houve uma falta de planejamento.
{% endhint %}

#### Reuniões

Procure sempre levar outro membro do projeto para as reuniões com o cliente, pois é sempre bom ter um ouvinte na reunião para garantir que nada se perca. Também é bom manter o controler de tudo que foi discutido nas reuniões para que o cliente não possa cobrar coisas que não pediu.

Para mudanças solicitadas pelo cliente (principalmente novas funcionalidades), evite de dar uma resposta na mesma hora ou ao final da reunião. Avise que irá pensar à respeito mesmo que tenha praticamente certeza de que a mudança será implementada.

### Revisão de PRs

Essa é uma questão delicada, muitas vezes você vai precisar usar um pouco do bom senso para balancear o aprendizado do membro com a entrega das issues no prazo. 

Ao revisar um PR e perceber que algumas mudanças devem ser feitas antes do merge, na maioria das vezes é recomendado que você solicite ao próprio membro que realize as mudanças,  procurando sempre deixar bem explicado para o membro o porquê daquela mudança ser necessária (Não sendo algo óbvio, como um bug) e, caso você tenha conhecimento, dar um caminho para o membro de como realizar essa mudança. 
Dessa forma, quando o membro passar por uma situação semelhante no futuro, ele mesmo irá resolver sem nem precisar de sua review, o que não aconteceria caso você tivesse simplesmente realizado a mudança e mergeado o PR. 

{% hint style="warning" %}
    Apesar de pedir para o próprio membro realizar as mudanças ser o ideal, é bom sempre ter em mente que isso pode atrasar um pouco o desenvolvimento do projeto.
{% endhint %}

{% hint style="warning" %}
    Também não esqueça de levar em consideração a sua própria disponibilidade, evitando tentar resolver tudo sozinho e acabar se sobrecarregando.
{% endhint %}

#### Final de projeto

Mais para o final do projeto, as coisas tendem a ficar meio caóticas com a correria para entregar o projeto dentro do prazo. Se for o caso, apesar de não ser muito recomendado, não tenha medo de colocar a mão na massa você mesmo. Para pequenas alterações (como feedbacks do cliente, ou detalhes que faltaram em PRs), muitas vezes vale mais você fazer direto do que passar para algum membro fazer, poupando bastante tempo no processo.

### Conheça seus membros

Conhecer os membros com os quais você está trabalhando no dia a dia é imprenscindível para uma boa gerência de projetos. Procure sempre ter saber como está a semana de cada membro, quando eles pretendem fazer suas issues, quais são suas dificuldades, facilidades e preferências. Com isso, você terá uma boa noção de quando oferecer ajuda e quais atividades passar para cada um. 
Não ache que você está sendo chato ao mandar uma mensagem para o membro, no dia seguinte ao que ele falou que estaria trabalhando, perguntando como está o andamento. Muitas vezes ele pode estar com algum problema que só seria descoberto no dia da reunião. 

Crie um ambiente agradável para o time, incentivando o pessoal a mandar dúvidas no canal e tirar dúvidas dos demais.

## Product Owner

O Product Owner é um papel do SCRUM fundamental para garantir uma boa comunicação com o cliente. Diferentemente do gerente do projeto, ele não terá responsabilidades técnicas, como revisão de código ou colocar a mão na massa durante o projeto. Sua principal função é ser a ponte entre os membros do projeto e o cliente, buscando sempre deixar claro para os desenvolvedores o quê o cliente quer, também deve comunicar ao cliente as dificuldades que estão sendo enfrentadas e as sugestões trazidas pela equipe, buscando sempre ser o mais transparente possível com o cliente. 

## Ambiente de produção e staging

O ambiente de produção é o espaço onde colocaremos o código da branch *production* para que ele possa ser acessado diretamente pelo cliente ou pelos usuários. Como gerente de projeto, é seu trabalho colocar o código da branch *production* no ambiente de produção ao final do projeto \(ou antes da data de entrega do projeto\). Para esse fim utilizaremos o [Docker](../docker/README.md), uma ferramenta que fornece um ambiente de virtualização para colocarmos o projeto.

Devido à complexidade do processo de colocar o código em produção, achamos melhor detalhar isso em uma [página específica](../docker/colocando-um-projeto-em-producao.md) do Gitbook. Lembre-se, também, que qualquer mudança requisitada pelo cliente só será perceptível **se o código estiver em produção**, de forma que **você deverá realizar esse processo regularmente** \(se esquecer de colocar novas features ou correções de features existentes em produção é uma excelente forma de **irritar** o cliente\).

O ambiente de staging é similar ao ambiente de produção, no entanto ele é considerado um *deploy temporário*, uma vez que não é uma versão apropriada para o uso dos usuários, é utilizado mais para testes e para mostrar as mudanças feitas para o cliente. Por ser uma versão mais para testes e não precisar de tantos recursos, geralmente não fazemos o deploy em staging em nosso servidor, mas sim utilizamos alguma ferramenta externa para tal finalidade, como o [heroku](../heroku.md) ou o [railway](https://railway.app/) para fazer o deploy da api do rails e o [netlify](https://www.netlify.com/) para fazer o deploy do front em react.
