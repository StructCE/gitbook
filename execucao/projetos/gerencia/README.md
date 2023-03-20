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

## Product Owner

O Product Owner é um papel do SCRUM fundamental para garantir uma boa comunicação com o cliente. Diferentemente do gerente do projeto, ele não terá responsabilidades técnicas, como revisão de código ou colocar a mão na massa durante o projeto. Sua principal função é ser a ponte entre os membros do projeto e o cliente, buscando sempre deixar claro para os desenvolvedores o quê o cliente quer e/ou precisa e também comunicar ao cliente as dificuldades que estão sendo enfrentadas e as sugestões trazidas pela equipe, buscando sempre ser o mais transparente possível com o cliente. 

## Ambiente de produção e staging

O ambiente de produção é o espaço onde colocaremos o código da branch *production* para que ele possa ser acessado diretamente pelo cliente ou pelos usuários. Como gerente de projeto, é seu trabalho colocar o código da branch *production* no ambiente de produção ao final do projeto \(ou antes da data de entrega do projeto\). Para esse fim utilizaremos o [Docker](./docker/README.md), uma ferramenta que fornece um ambiente de virtualização para colocarmos o projeto.

Devido à complexidade do processo de colocar o código em produção, achamos melhor detalhar isso em uma [página específica](./docker/colocando-um-projeto-em-producao.md) do Gitbook. Lembre-se, também, que qualquer mudança requisitada pelo cliente só será perceptível **se o código estiver em produção**, de forma que **você deverá realizar esse processo regularmente** \(se esquecer de colocar novas features ou correções de features existentes em produção é uma excelente forma de **irritar** o cliente\).

O ambiente de staging é similar ao ambiente de produção, no entanto ele é considerado um *deploy temporário*, uma vez que não é uma versão apropriada para o uso dos usuários, é utilizado mais para testes e para mostrar as mudanças feitas para o cliente. Por ser uma versão mais para testes e não precisar de tantos recursos, geralmente não fazemos o deploy em staging em nosso servidor, mas sim utilizamos alguma ferramenta externa para tal finalidade, como o [heroku](../heroku.md) ou o [railway](https://railway.app/) para fazer o deploy da api do rails e o [netlify](https://www.netlify.com/) para fazer o deploy do front em react.
