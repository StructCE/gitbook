# GitHub com Discord

A integração entre ambas as ferramentas permite com que certas ações, realizadas em um repositório do GitHub, sejam retransmitidas para um canal de texto do Discord

## Como relizar a integração?

### Criação do webhook

- O primeiro passo é criar no discord o canal de texto no qual será relizada a integração;
- Com o canal de texto criado, agora você precisará clicar na engrenagem que aparece quando colocado o ponteiro do mouse sobre o canal, onde está escrito **editar canal**;
- Então, aparecerá uma janela de configurações do canal desejado, e você irá em **Integrações**, na barra lateral esquerda;
- Em _Integrações_, estará presente a opção de manipulação de webhooks no canal desejado, então você irá clicar em **Criar webhook**, caso este seja o primeiro webhook a ser criado no canal, ou em _Ver webhooks_, caso já exista algum, e, neste último caso, irá criar um novo webhook;
- Com o novo webhook criado, você irá escolher o canal de texto criado para a integração e irá editar o nome da forma que desejar, lembrando que este será o bot que emitirá mensagens sobre alterações no repositório do github desejado;
- Em seguida, clique em **Copiar a URL do webhook**, para utilizarmos nos próximos passos, e, por fim, em **Salvar alterações**, no botão verde logo abaixo.

### Utilização do webhook

- Agora vamos para o seu repositório do GitHub, o qual você deseja emitir os alertas;
- Com o repositório aberta no GitHub, você primeiro irá em **Settings**, na barra horizontal acima, e posteriormente irá em **Webhooks**, na barra lateral esquerda;
- Na sessão de _Webhooks_, você irá agora em **Add webhook**;
- Dessa forma, será exigido que você coloque sua senha do GitHub. Basta inserir sua senha e finalmente você poderá configurar a integração pelo lado do GitHub;
- Na sessão de _Add webhook_, você irá colar, em _Payload URL_, aquele mesmo link copiado no Discord, quando você clicou em **Copiar a URL do webhook**; porém, será necessário adicionar, ao final do link, o trecho "/github" sem as aspas;

Exemplo de como ficará o link:
`https://discord.com/api/webhooks/12345678910111213/Abcd_E_Fghijklmnopqrs-1234-tuvwxyz/github`

- Em _Content type_, você irá escolher **application/json**;
- em _Which events would you like to trigger this webhook?_, você poderá escolher quais ações no repositório serão alertadas no discord, de acordo com suas preferências;
- Finalmente, basta clicar em **Add webhook**

Está pronto! Agora mudanças no seu repositório do GitHub irão ser alertadas no seu canal de texto do Discord!!
