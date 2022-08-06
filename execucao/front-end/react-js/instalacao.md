# Instalação

Para iniciar um projeto react, precisamos instalar algumas coisas:

## Node e npm

Browsers nativamente tem capacidade de rodar javascrpit. Para rodar javascript localmente, podemos usa o Node.js. Além disso, podemos instalar e controlar o versionamento de pacotes pelo npm.

### Windows

Acesse o [site oficial](https://nodejs.org/en/) e baixe o instalador oficial recomendado. Ele irá instalar o node e o npm ao mesmo tempo.

### Linux

Podemos instalar o Node.js com o seguinte comando:

```Bash
sudo apt install nodejs
```

Por padrão o npm é instalado com o node. Para conferir as instalações, rode:

```Bash
node -v
```

Output:

```Bash
v16.12.2
```

```Bash
npm -v
```

Output:

```Bash
8.5.5
```

{% hint style="info" %}
Caso o npm não tenha sido instalado, basta rodar o comando:

```Bash
sudo apt install npm
```

{% endhint %}

## Yarn

O yarn é um gerenciador de pacotes similar ao npm, e é o utilizado em nossa EJ.

### Windows e Linux

Para instalar o yarn basta rodar:

```Bash
npm install --global yarn
```

E para verificar a instalação, rode:

```Bash
yarn -v
```

Output:

```Bash
3.2.2
```
