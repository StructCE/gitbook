# Guias Geralmente Utilizados

Nessa seção apresentaremos alguns tópicos ou referências que são interessantes de serem passados aos trainees durante o PT.

- [Tutorial Git](../../execucao/git/README.md)
- [Instalação Ruby e rails](../../execucao/ruby-on-rails/instalacao.md)
- [Tutorial ruby, rubymine e vscode](https://youtu.be/LJ5GhhaGlog)
- [Dual Boot](#dual-boot)
- Instalando e utilizando o PostgreSQL
    - [Instalação e utilização (ubuntu 20.04)](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-on-ubuntu-20-04-pt)
    - [Integração com o rails (ubuntu 18.04)](https://www.digitalocean.com/community/tutorials/how-to-use-postgresql-with-your-ruby-on-rails-application-on-ubuntu-18-04)
    - [Instalação e pgAdmin 4 (Windows 10)](https://www.youtube.com/watch?v=e1MwsT5FJRQ)
- [Instalação do yarn e do npm](#requisitos-do-javascript)

## Dual Boot

{% hint style="warning" %}
Antes de passar esse guia aos trainees, verifique se ele está atualizado.
{% endhint %}

### O que é?

Para os trainees, principalmente os calouros do curso, que podem estar meio perdidos, o Dual Boot é a capacidade de escolha entre dois sistemas operacionais instalados no mesmo compuador assim que ele é ligado. Na realidade, um computador pode ter vários sistemas operacionais instalados, sem que um interfira no outro, desde que os procedimentos sejam feitos corretamente.

No caso do Linux, sistema que sugerimos que seja utilizado para programação, a instalação é feita através de um pendrive bootável, ou seja, um pendrive utilizado como mídia de instalação.

{% hint style="info" %}
Não é obrigatório que os trainees utilizem o linux ou façam um dual boot em seu computador, porém muitas coisas são mais fáceis nesse sistema do que no Windows, além de que a maioria dos membros da Struct utilizam esse sistema, o que pode dificultar para ajudar os trainees a resolver problemas específicos do Windows.
{% endhint %}

### Pendrive Bootável

Existem diversas distribuições do linux que os trainees podem optar por utilizar. Entre as mais famosas temos o Ubuntu, o Linux-Mint e o PopOS, sendo as 3 ótimas para ajudá-los nessa jornada, vai mais de gosto pessoal de cada um. Segue abaixo os links para download de cada uma dessas distros, no caso do linux mint, escolha alguma versão que tem a bandeira do Brasil. Já no caso do Ubuntu e do PopOs, é recomendado a instalação das versões LTS (Long Term Support) que são lançadas a cada 2 anos e têm cerca de 5 anos de suporte (como 20.04 LTS):

- [Linux Mint](https://linuxmint.com/edition.php?id=284)
- [Ubuntu](https://ubuntu.com/download/desktop)
- [PopOs](https://pop.system76.com/)

Após o download da distro escolhida, vamos precisar de um pedrive para que sejmos capazes de iniciar e instalar o linux corretamente em seu computador. Existem diversas ferramentas para transformar nosso pendrive em um pendrive bootável, nesse [tutorial](https://youtu.be/bGrWprBkxvo) é utilizado o "Rufus". Depois de instalado, abra o programa, selecione a distro escolhida e o pendrive para continuar.

{% hint style="danger" %}
**Todos** os dados do pendrive serão **apagados** nesse processo, por isso certifique-se de que não há nada de importante nele ou faça um backup antes de prosseguir. 
{% endhint %}

### Instalação do Linux

{% hint style="warning" %}
Recomendamos que copie seus arquivos para um HD externo ou faça algum tipo de back-up para caso ocorra algum erro no seu dual boot. Não é comum, porém pode acontecer de todos os arquivos do computador serem perdidos, portanto leiam todo o texto e assistam aos vídeos com cuidado antes de fazer qualquer coisa!!!
{% endhint %}

Depois que o pendrive bootável já estiver pronto com a distribuição escolhida, abra o Gerenciamento de Disco do Windows (basta pesquisar isso na barra de tarefas, provavelmente irá aparecer algo como "Criar e formatar partições do disco rígido") e selecione o seu HD (ou SSD, se for o caso), clique com o botão direito e selecione "diminuir volume", com isso ele abrirá um painel com a memória que deseja desalocar do Windows. Sugiro que separe ao menos 40GB para o Linux (40000 MB) e então clique em "diminuir", feito isso, verá que a memória separada estará como espaço livre, e é exatamente assim que queremos que ela esteja. Deixaremos aqui um [vídeo](https://www.youtube.com/watch?v=tlNP2JPl0rw) que pode auxiliar no uso do Gerenciamento de Disco.

#### BIOS

Agora é a parte mais complicada do processo: fazer o computador iniciar pelo Pendrive, para isso iremos destrinchar essa parte para facilitar o entendimento:

{% hint style="info" %}
Nos passos abaixo, algumas coisas devem variar de acordo com o modelo de seu computador, mas a princípio são bem parecidas. Caso pareça muito diferente, procure algum tutorial específico para o seu computador de como fazer boot pelo pendrive.
{% endhint %}

1. Com o pendrive bootável conectado ao computador, desligue-o;
2. Ligue o computador e pressione a tecla *F2* (ou *F12* dependendo do modelo) diversas vezes enquanto ele incia, isso deverá levá-lo a "BIOS" de seu computador;
3. Com a BIOS aberta, vá em "advanced" e ative "USB3 Wake-up";
4. Vá em "boot" e desative "secure boot control", "fast bios mode" e "pxeoprom";
5. Ainda em Boot, procure a opção "OS Mode Control" e selecione "CSM and UEFI OS";
6. Vá em "Boot Device Priority" e como "Boot option #1" selecione a opção que não é o HD (ou SSD), pode ter o nome de "General UDisk", "USB Flash" ou algo diferente do que já está lá;
7. Clique em "save configuration and reset". Com isso, seu computador deve fazer boot com o pendrive, o que permitirá a instalação do Linux;  
Segue um [vídeo](https://www.youtube.com/watch?v=_pdKLVtrw-Q) explicando o uso da BIOS em notebooks da Samsung.

#### Flash drive Boot e instalação

Se tudo tiver funcionado corretamente no passo anterior, agora seu computador deve ter inciado via pendrive, ou seja, sem sinal do windows por aqui. Essa parte vai ser um pouco diferente a depender da distro do Linux que foi escolhida. Independentemente, escolha a língua que se sentir mais à vontade e escolha o layout de seu teclado.

Em todas as opções, vá em "Instalação avançada", "custom" ou "something else", **NUNCA** vá em apenas baixar o linux, pois isso pode acabar instalando por cima do Windows, fazendo com que você perca todos os seus arquivos e o próprio Windows. Mesemo que seja tentador apenas clicar em "instalar ao lado do windows 10", é bom evitar essa opção, vá em instalação avançada mesmo, pois isso nos permite ter mais controle do processo como um todo.

Após clicar em instalação avançada, selecione a partição de memória não alocada/espaço livre, que será aquela que desalocamos no gerenciador de disco anteriormente, e vá em "ponto de motagem" e selecione "/". Ainda nessas configurações vá em "Usar como" e selecione "sistema de arquivo com Journaling ext4". Pronto, agora o que era espaço livre é uma nova partição de seu HD/SSD, selecione-a e clique em "instalar".

Segue abaixo um tutorial dessa etapa em cada uma das distribuições do linux citadas anteriormente:

- [Linux-mint](https://youtu.be/KV6KiveQTpI?t=504)
- [Ubuntu](https://www.youtube.com/watch?v=45--PnNFATU)
- [PopOs](https://youtu.be/EXZ7_DVxztQ?t=360)

## Requisitos do JavaScript

No rails, as bibliotecas (gems) eram gerenciadas pela gem + bundler, já no JavaScript, é utilizado o yarn, que é uma ferramenta de distribuição das bibliotecas de JS. Para instalar o yarn, primeiramente é necessário instalar o npm, que é outro gerenciador de pacotes, porém não é tão estável quanto o yarn. 

### Npm e NodeJS

Para instalar o npm, basta instalarmos o NodeJS (um compilador para rodar JavaScript fora do browser), no ubuntu e sistemas baseados no Debian é bem simples, apenas entre no terminal e rode esses dois comandos:

```
$ curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -

$ sudo apt-get install -y nodejs
```

Para conferir se deu tudo certo rode os comandos `$ node -v` e `$ npm -v` que devem retornar as versões instaladas do node e do npm, respectivamente. Caso seu sistema operacional seja diferente e os comandos acima não funcionem, no site do [nodejs.org](https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions) há a explicação para a instalação em diferentes tipos de distribuições e sistemas.

### Yarn

A instalação do yarn pode ser feita de [diversas maneiras](https://classic.yarnpkg.com/en/docs/install#windows-stable), porém **não instale o yarn por snap**, uma vez que isso instala uma versão diferente (0.X.X+git) que não funciona. A forma mais fácil de instalá-lo é pelo próprio npm mesmo, apenas rode o comando `$ npm install --global yarn` e teste se deu certo com o `$ yarn -v`.
