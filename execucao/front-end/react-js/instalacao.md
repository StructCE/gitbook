# Instalação

Para iniciar um projeto react, precisamos instalar algumas coisas. Primeiro o Node e npm, e depois o yarn (no final desse guia).

## Node e npm

Browsers nativamente tem capacidade de rodar javascrpit. Para rodar javascript localmente, podemos usar o Node.js. Além disso, podemos instalar e controlar o versionamento de pacotes pelo npm (ou yarn, como visto mais a frente).
Para instalar essas ferramentas, utilizaremos o `nvm` (node version manager)

### Windows

#### windows nvm

Essa não é a mesma coisa que o `nvm`, mas é o recomendado para controlar versão do node para windows.

Basta entrar em [repositório nvm-windows](https://github.com/coreybutler/nvm-windows#installation--upgrades), clicar em "`Download now`", selecionar a última versão e intalar.
Para verificar a instalação, no terminal digitar:

```bash
nvm -v
```

#### node e npm

Para instalar a última versão do node com _long term support_ (_lts_), use:

```bash
nvm install lts
```

Esse comando também instala o npm

Para verificar as instalações,

```bash
node -v
npm -v
```
Que deve ter como outupt algo semelhante a
```bash
v16.18.0
8.19.2
```


### Linux

#### nvm


Para instalar, basta rodar no terminal:
```bash
sudo apt install curl 
curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash
```

O script para instalar o nvm cria depende do login do usuário corrente. Por isso, você pode deslogar e logar novamente pra poder utilizar o nvm, ou usar o script:

```bash
source ~/.bashrc
```

Para verificar a instalação, rodar

```bash
nvm --version
```
Que deve ter como output algo semelhante a:
```bash
0.35.0
```


#### node e npm

Para instalar a última versão do node com _long term support_ (_lts_), use:

```bash
nvm install --lts
```

Esse comando também instala o npm

Para verificar as instalações,

```bash
node -v
npm -v
```
Que deve ter como outupt algo semelhante a
```bash
v16.18.0
8.19.2
```

## Yarn

O yarn é um gerenciador de pacotes similar ao npm, e é o utilizado em nossa EJ.

### Windows e Linux

Para instalar o yarn basta rodar:

```bash
npm install --global yarn
```

E, para verificar a instalação, rode:

```bash
yarn -v
```

Output:

```bash
3.2.2
```
