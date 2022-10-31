# Gerência de projetos

O gerente de um projeto possui funções essenciais à qualidade de vida de um projeto, como a criação do projeto em si, a gerência das *sprints* do projeto e a comunicação dos detalhes do projeto para os outros membros de equipe nas reuniões gerais. Em suma, o gerente do projeto conduz a execução do projeto, tomando as medidas necessárias para que seu desenvolvimento seja bem sucedido.

Está pagina contém as informações necessárias para se gerenciar um projeto de maneira adequada.

## Reuniões gerais

O gerente de um projeto também tem o trabalho de participar das reuniões gerais \(RGs\) da Struct para informar aos outros membros da empresa júnior \(em especial, o presidente e o diretor de projetos\) o estado de desenvolvimento do projeto. Nessa hora, o gerente deve destacar de forma bem resumida se o desenvolvimento do projeto está progredindo de maneira adequada, se há necessidade de mais pessoas serem alocadas no projeto e se algo de anormal está acontecendo com o projeto.

Caso o gerente de um projeto não possa comparecer à reunião geral, ele deve instruir algum outro membro do projeto que estará na RG à realizar essa função. Caso isso não seja possível, o gerente deve enviar uma mensagem breve no *Slack* que detalhe esses fatores.

## Ambiente de produção e staging

O ambiente de produção é o espaço onde colocaremos o código da branch *production* para que ele possa ser acessado diretamente pelo cliente ou pelos usuários. Como gerente de projeto, é seu trabalho colocar o código da branch *production* no ambiente de produção ao final do projeto \(ou antes da data de entrega do projeto\). Para esse fim utilizaremos o [Docker](./docker/README.md), uma ferramenta que fornece um ambiente de virtualização para colocarmos o projeto.

Devido à complexidade do processo de colocar o código em produção, achamos melhor detalhar isso em uma [página específica](./docker/colocando-um-projeto-em-producao.md) do Gitbook. Lembre-se, também, que qualquer mudança requisitada pelo cliente só será perceptível **se o código estiver em produção**, de forma que **você deverá realizar esse processo regularmente** \(se esquecer de colocar novas features ou correções de features existentes em produção é uma excelente forma de **irritar** o cliente\).

O ambiente de staging é similar ao ambiente de produção, no entanto ele é considerado um *deploy temporário*, uma vez que não é uma versão apropriada para o uso dos usuários, é utilizado mais para testes e para mostrar as mudanças feitas para o cliente. Por ser uma versão mais para testes e não precisar de tantos recursos, geralmente não fazemos o deploy em staging em nosso servidor, mas sim utilizamos alguma ferramenta externa para tal finalidade, como o [heroku](../heroku.md) ou o [railway](https://railway.app/) para fazer o deploy da api do rails e o [netlify](https://www.netlify.com/) para fazer o deploy do front em react.
