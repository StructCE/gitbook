# Boas práticas durante o projeto

## Organização

- Mantenha o controle de tudo que falta e do que já está feito;
- Se uma issue for mergeada sem estar 100%, anote o qe ficou faltando ou crie uma nova issue;

## Relação com

### Cliente

#### Não deixe o cliente no escuro

Esse tópico entra um pouco no tópico anterior. Em um cenário nada ideal, existe a possibilidade de você como gerente se deparar com uma situação bem chata: não será possível entregar o projeto dentro do prazo. 

Mas o que devemos fazer agora? Tentamos correr atrás e fazer um milhão de coding days seguidos para tentar colocar o projeto de volta nos trilhos? Adicionamos mais membros ao projeto? Paramos a empresa inteira para fazer um mutirão para entregarmos o projeto? Bem, já adianto que, na maioria dos casos, essas possibilidades não irão funcionar, inclusive podem ter o efeito reverso e acabar atrasando o projeto ainda mais, visto que vão acabar desgastando os desenvolvedores.

Sendo assim, antes de sair procurando soluções para tentar cumprir com um prazo irreal, procure sempre entrar em contato com o cliente, explicando desde cedo os problemas que vocês estão enfrentando e já prepará-lo para um possível atraso, podendo até chegar a um acordo para realizar uma entrega inicial parcial, mesmo com algumas funcionalidades faltando.

{% hint style="info" %}
    Uma possível alternativa para acelerar o desenvolvimento do projeto é introduzir os coding moments na rotina da equipe, que são basicamente momentos em que os próprios membros do projeto se reúnem para codar durante a semana. Isto pode contribuir bastante para a integração dos membros e para tornar o time mais produtivo no geral
{% endhint %}

{% hint style="warning" %}
    Ao falar sobre atrasos com o cliente, tente focar mais nas questões técnicas que causaram o atraso e evite dizer coisas como "está atrasando pois estamos em final de semestre na universidade", dando a impressão que houve uma falta de planejamento.
{% endhint %}


#### Reuniões

Procure sempre levar outro membro do projeto para as reuniões com o cliente, pois é sempre bom ter um ouvinte na reunião para garantir que nada se perca. Também é bom manter o controler de tudo que foi discutido nas reuniões para que o cliente não possa cobrar coisas que não pediu.

Para mudanças solicitadas pelo cliente (principalmente novas funcionalidades), evite de dar uma resposta na mesma hora ou ao final da reunião. Avisa=a que irá pensar à respeito mesmo que tenha praticamente certeza de que a mudança será implementada.

### Membros

Conhecer os membros com os quais você está trabalhando no dia a dia é imprenscindível para uma boa gerência de projetos. Procure sempre ter saber como está a semana de cada membro, quando eles pretendem fazer suas issues, quais são suas dificuldades, facilidades e preferências. Com isso, você terá uma boa noção de quando oferecer ajuda e quais atividades passar para cada um.
Não ache que você está sendo chato ao mandar uma mensagem para o membro, no dia seguinte ao que ele falou que estaria trabalhando, perguntando como está o andamento. Muitas vezes ele pode estar com algum problema que só seria descoberto no dia da reunião. 

É importante também que os desenvolvedores estejam em comunicação constante entre si, e é isso que a *daily* garante. Eles devem entender o projeto e se sentirem incluídos na tomada de decisão, nem que seja somente porque foi explicada a motivação por trás das decisões.

Crie um ambiente agradável para o time, incentivando o pessoal a mandar dúvidas no canal e tirar dúvidas dos demais.

### Diretoria de projetos

Comunique sempre o andamento do projeto à diretoria de projetos. Caso precise de ajuda com alguma coisa, seja numa decisão ou numa ação, também não hesite em perguntar. 

## Revisão de PRs

Essa é uma questão delicada, muitas vezes você vai precisar usar um pouco do bom senso para balancear o aprendizado do membro com a entrega das issues no prazo. 

Ao revisar um PR e perceber que algumas mudanças devem ser feitas antes do merge, na maioria das vezes é recomendado que você solicite ao próprio membro que realize as mudanças,  procurando sempre deixar bem explicado para o membro o porquê daquela mudança ser necessária (Não sendo algo óbvio, como um bug) e, caso você tenha conhecimento, dar um caminho para o membro de como realizar essa mudança. 
Dessa forma, quando o membro passar por uma situação semelhante no futuro, ele mesmo irá resolver sem nem precisar de sua review, o que não aconteceria caso você tivesse simplesmente realizado a mudança e mergeado o PR. 

{% hint style="warning" %}
    Apesar de pedir para o próprio membro realizar as mudanças ser o ideal, é bom sempre ter em mente que isso pode atrasar um pouco o desenvolvimento do projeto.
{% endhint %}

{% hint style="warning" %}
    Também não esqueça de levar em consideração a sua própria disponibilidade, evitando tentar resolver tudo sozinho e acabar se sobrecarregando.
{% endhint %}

### Final de projeto

Mais para o final do projeto, as coisas tendem a ficar meio caóticas com a correria para entregar o projeto dentro do prazo. Se for o caso, apesar de não ser muito recomendado, não tenha medo de colocar a mão na massa você mesmo. Para pequenas alterações (como feedbacks do cliente, ou detalhes que faltaram em PRs), muitas vezes vale mais você fazer direto do que passar para algum membro fazer, poupando bastante tempo no processo.
