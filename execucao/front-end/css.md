# CSS
## Sobre o CSS
CSS, em inglês Cascading Style Sheets, é uma linguagem de estilização usada para ajustar o HTML. Ela é composta de seletores e propriedades(regras) e a sintaxe geral é:
```CSS
seletor {
    propriedade: valor;
}
/*
Comentário
*/
```
## Como integrar o CSS e o HTML
Existem 3 formas de colocar o CSS para estilizar o HTML:
* Como atributo no elemento
### Exemplo
```HTML
<body>
    <p style="font-size: 12px; color: red;">Um parágrafo de exemplo</p>
</body>
```
* Dentro do elemento Style
### Exemplo
```HTML
<head>
    <style>
        p {
            font-size: 12px;
            color: red;
        }
    </style>
</head>
<body>
    <p>Um parágrafo de exemplo</p>
</body>
```
* Em outro arquivo
### No arquivo HTML:
```HTML
<head>
    <link rel="stylesheet" type="text/css" href="file.css">
</head>
<body>
    <p>Um parágrafo de exemplo</p>
</body>
```
### Em um arquivo .css:
```CSS
p {
    font-size: 12px;
    color: red;
}
```
{% hint style="info" %}
    OBS: a tag link é utilizada para integrar o arquivo file.css com o HTML.
{% endhint %}

{% hint style="info" %}
    OBS2: a forma mais apropriada para integrar é utilizando o arquivo separado. 
{% endhint %}

## Seletores
Existem alguns tipos de seletores: por tag HTML, por classe e por id.
### Tag Selector
As regras dentro desse seletor se aplicam a todas as tags HTML desse tipo. Exemplos:
```CSS
/*
Todos os parágrafos p ficarão com a cor azul de texto
*/
p {
    color: blue;
}
/*
Todos os div ficarão com a cor de fundo amarela
*/
div {
    background-color: yellow;
}
```
### Class Selector
As regras dentro desse seletor se aplicam a todas as tags HTML que tenham a classe seletora. Se coloca um "." antes da palavra, para indicar que é uma classe.
```CSS
/*
Todos os elementos com a classe title ficarão com o tamanho de texto de 48px.
*/
.title {
    font-size: 48px;
}
```

### Id Selector
As regras dentro desse seletor somente se aplicarão à tag que tem o id igual ao id seletor. Se coloca um "#" antes da palavram, para indicar que é um id.
```CSS
/*
O elemento com o id my_id terá a largura de 100% do elemento pai
*/
#my_id {
    width: 100%;
}
```

### Combinando Seletores
É possível combinar mais de um seletor ou especificar seletores para alcançar mais elementos ou elementos mais específicos.

#### Multiplos Seletores
Pode-se colocar múltiplos seletores para as mesmas regras. As regras **serão aplicadas para todos as tags selecionadas**.
```CSS
/*
Esse código aplica a regra de padding(espaço entre o elemento e sua borda) para todas as tags button e p, além de aplicar para tags que tenham a classe some_class
*/
button, .some_class, p {
    padding: 10px;
}
```

#### Seletores Específicos
Para a tag ser estilizada, ela **precisa participar dos dois ou mais grupos de seletores**. Pode ser uma tag e uma classe, ou duas classes ou mais.
```CSS
/*
Apenas um div que tenha a classe specific irá ter sua cor de fundo mudada para #FFFFFF(branco em hexadecimal)
*/
div.specific {
    background-color: #FFFFFF;
}
/*
Apenas para um elemento que tenha as classes dark, large e spaced essas regras se aplicarão
*/
.dark.large.spaced {
    color: black;
    width: 200px;
    margin: 20px;
}
```
#### Seletores Descedentes
Uma relação de descendência entre os seletores. A sintaxe é
```CSS
seletor1 seletor2 {
    regras...
}
```
Onde o seletor1 representa o "elemento pai" do seletor2.
##### Exemplo: arquivo HTML
```HTML
<div class="links-container">
    <a>Link 1</a>
    <a>Link 2</a>
</div>
```
##### Exemplo: arquivo CSS
```CSS
/*
Apenas links(tags a) dentro de um elemento que contenha a classe links-container irão ter a decoração de texto retirada e a cor mudada para preto.
*/
.links-container a {
    text-decoration: none;
    color: black;
}
```

#### Caso especial: Descendente direto
Coloca-se ">" para que só se peguem os descendentes diretos do "elemento pai".
##### Exemplo usando o exemplo HTML acima:
```CSS
/*
Nesse caso, mesmo que tivesse outro div dentro do div de links-container e dentro desse div tivesse um link(tag a), apenas os links 1 e 2 serão estilizados.
*/
links-container > a {
    text-decoration: none;
    color: black;
}
```

#### Seletor de tudo(*)
Para selecionar todas as tags HTML é possível usar o "*". A aplicação seria para pegar todas as "crianças" diretas de um elemento pai:
```CSS
/*
Todos os elementos filhos diretos do elemento com a classe links-container teriam seu estilo alterado.
*/
links-container > * {
    color: black;
}
```

### Precedência
Quando existem regras conflitantes entre si, por exemplo 2 regras mudando a cor de um texto, existe uma ordem de precedência que o CSS obedece ao estilizar o HTML:
1. A regra mais específica
2. Seletor de Id
3. Seletor de Classe
4. Regras que vierem depois de outras que estão antes no arquivo

{% hint style="info" %}
    OBS: pode-se usar !important depois de uma regra para anular qualquer outra, independentemente da precedência explicada anteriormente.
{% endhint %}

## Propriedades
São as regras que serão passadas aos elementos selecionados pelos seletores. Antes de falarmos das propriedades, falaremos de algumas unidades utilizadas nessas regras.
### Unidades
No HTML e CSS existem várias unidades que serão utilizadas para definir o espaço no site. Entre elas, temos:
* Pixel(px)
* rem
* vw e vh
* %

#### Pixel
É a unidade mais comum de medição. Representa um pixel na tela(depende da tela utilizada).
##### Exemplo
![Relação pixels](/imagens/pixel.png)

#### Rem
É uma unidade relativa ao tamanho da fonte do elemento raiz(html, body), ou seja, é bem útil para padronizar o site. Na maioria dos browsers dos computadores, 1rem equivale a 16px.

#### Vw e Vh
São unidades relativas à proporção da tela que o usuário está usando. Vw significa viewport width, ou seja, está relacionada a uma porcentagem da largura da tela. Já Vh é a viewport height, está relacionada a uma porcentagem da altura da tela.

#### %
Como o símbolo já sugere, ele representa uma porcentagem do "elemento pai".

### Propriedades relativas a texto

#### Font-size
É o tamanho da fonte do texto. Para o exemplo utilizado na explicação sobre o pixel, foi utilizada essa propriedade para definir o tamanho do texto. Os valores possíveis são as unidades previamente explicadas ou valores padrão: small, medium, large, ...etc.

#### Line-height
É o espaço entre as linhas do texto. Ela será multiplicada pelo tamanho da fonte(font-size). São utilizadas as unidades de medida.

#### Text-align
Alinhamento do texto. Pode ter os valores de: left, right, center, justify e justify-all.

#### Text-decoration
Decoração do texto, pode ser underline, overline, line-through ou none.

#### Font-weight
É quão negrito o texto deve ficar. São utilizadas medidas de 100 a 900, valores padrão: normal(400), bold(700) ou ainda valores relativos como bolder(mais negrito) e lighter(menos negrito).

#### Font-family
É o fonte do texto. Podem ser colocados vários valores em sequência(font-family: "value1", "value2", ..., value;) para caso alguma das fontes não seja encontrada a seguinte ser implementada no texto. Tem alguns valores padrão como serif, sans-serif, monospace, cursive e fantasy; porém é possivel adicionar uma fonte externa utilizando o seguinte código no css:
```css
@font-face {
    font-family: name;
    src: url('url');
}
```
Para isso, é preciso ter a fonte em um arquivo do tipo fonte(.tff) e que ele esteja adicionado no projeto. Assim, o "name" seria o nome dado à fonte(que será utilizado para definir essa fonte nos outros textos) e o 'url' seria o caminho relativo do arquivo do tipo fonte no projeto.

Outra forma é utilizando fontes externas, é só importá-las utilizando a tag \<link/\> do html. Um exemplo de fácil uso é o google fonts:

```html
<head>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inconsolata:wght@200&display=swap" rel="stylesheet">
</head>
```
Para esse exemplo em específico, podemos usar a fonte importada normalmente no css:

```css
p {
    font-family: 'Inconsolata', monospace;
}
```
{% hint style="info" %}
    Ambos os códigos foram tirados do próprio site do [Google Fonts](https://fonts.google.com/specimen/Inconsolata)
{% endhint %}

#### Color
É a cor do texto. Pode ser:
* Um dos valores padrão como "blue" e "transparent";
* rgb(significa red green blue, uso: rgb(valor1, valor2, valor3), onde o valor varia de 0 a 255);
* rgba(o mesmo que rgb só que o "a" significa a transparência, uso: rgba(valor1, valor2, valor3, valor4), onde o valor varia de 0 a 255)
* hexadecimal(uso: #valor, onde o valor é em hexadecimal)

### Propriedades de containers

#### Background-color
Cor do fundo do container. Os valores são os mesmo aplicados a propriedade "color".

#### Background-image
Propriedade utilizada para colocar uma imagem no fundo no container. Propriedades relacionadas:
* Background-repeat: repeat/repeat-x/repeat-y/no-repeat; É usado para definir o que fazer caso a imagem não seja do tamanho do container.
* Background-size: contain/cover/width/height; É usado para definir como a imagem vai cobrir o container
* Background-position: center/x/y; É usado para definir a posição da imagem no fundo

#### Border
É um conjunto de 3 outras propriedades relacionadas à borda do elemento: 
* border-width: usa as unidades de medida para definir qual é o tamanho da borda
* border-style: tem alguns valores padrão: none, hidden, solid, dotted, dashed, groove, ridge, inset e outset
* border-color: tem os mesmos valores que "color".

{% hint style="info" %}
    OBS: Border-radius é uma outra propriedade relacionada à borda que deve ser definida separadamente para arredondar os cantos das bordas. O valor é de unidade de medida. 
{% endhint %}

{% hint style="info" %}
    OBS2: Todas essas propriedades podem ser definidas para apenas um dos cantos usando border-(left/right/top/bottom) ou ainda definir para os 4 cantos de uma vez da seguinte forma:
{% endhint %}

    * 1 valor(será aplicado para todos os 4)
    * 2 valores(top e bottom para o primeiro valor, left e right para o segundo)
    * 4 valores(top, right, bottom e left) 

#### Margin
É uma propriedade que define quanto de espaço o elemento irá "empurrar" os elementos adjacentes. Usam-se as unidades de medida. Podem ser aplicadas as regras da [OBS2 da Border](#obs2-todas-essas-propriedades-podem-ser-definidas-para-apenas-um-dos-cantos-usando-border-leftrighttopbottom-ou-ainda-definir-para-os-4-cantos-de-uma-vez-da-seguinte-forma) para definir para um dos 4 cantos.

#### Padding
É a propriedade que define quanto de espaço entre o elemento e a borda tem que existir. Usam-se as unidades de medida.
Podem ser aplicadas as regras da [OBS2 da Border](#obs2-todas-essas-propriedades-podem-ser-definidas-para-apenas-um-dos-cantos-usando-border-leftrighttopbottom-ou-ainda-definir-para-os-4-cantos-de-uma-vez-da-seguinte-forma) para definir para um dos 4 cantos.

#### Width e Height
São duas propriedades que definem qual será o tamanho do elemento. Quando se coloca apenas uma delas, a outra é calculada automaticamente. Os valores podem ser:
* Valores de unidade de medida
* Valores padrão como max-content, min-content e fit-content

{% hint style="info" %}
    OBS: os prefixos max- e min- podem ser usados antes de width e height para definir outras propriedades que definem um tamanho máximo ou mínimo para o elemento.
{% endhint %}

## The Box Model
As 4 últimas propriedades fazem parte do Box Model:
![Box Model](/imagens/box_model.png)
### Propriedade Box-sizing
Define se as propriedades de height e width vão considerar apenas o conteúdo da caixa e padding e border são "adicionais"(content-box) ou vão considerar a padding e a border também, sendo o tamanho total considerado para o cálculo dessas propriedades(border-box).
### Propriedades de Overflow
Às vezes os elementos são grandes demais para a tela, e para essa e outras razões existe a propriedade de overflow, que pode deixar que os elementos passem do container que estão de alguma forma, que depende do valor passado. Valores possíveis:
* auto: se necessário, será adicionado um scroll
* hidden: a parte que está além dos limites do elemento será escondida
* visible: o overflow fica visível
* scroll: adiciona um scroll, mesmo que não seja necessário

{% hint style="info" %}
    OBS: É possível utilizar essa propriedade separadamente para eixo x e y, utilizando overflow-x ou overflow-y.
{% endhint %}

## Propriedade Display
Essa propriedade define como o elemento será disposto na tela. Existem 2 tipos principais de elemento no HTML:
* Elementos de bloco(block): esses por padrão ocupam o espaço de tal forma que não é possível nenhum elemento ficar à sua esquerda ou direita sem o uso de outras propriedades. Eles respeitam as propriedades de width e height.
* Elemento do tipo linha(inline): esses se ajustam de forma que eles podem ficar na mesma linha que outros elementos inline ou inline-block, como veremos depois. Eles não respeitam as propriedades de width e height.

Dessa forma, motivado a colocar um width ou height em um elemento inline, foi-se criado o tipo "inline-block", que tem as mesmas características do tipo block, porém pode ficar ao lado de outros elementos.

Outra valor possível para a propriedade Display é o "none", que basicamente retira o elemento da página. Ele pode ser útil para fazer um site responsivo, pois quando a tela é muito pequena é possível retirar alguns elementos e adicionar outros mais adequados.

## Display flex
Por último, um valor para o display pode ser "flex", que define o elemento como um container(a flexbox) e os seus "elementos filhos"(flex-itens) serão organizados de alguma forma inteligente, dependendo do valor de algumas propriedades relacionadas.

Entre essas propriedades temos:

* flex-flow: é uma propriedade da flexbox que engloba outras 2(flex-flow: flex-direction flex-wrap): 
   * flex-direction: define a direção em que os itens dentro da flexbox vão ser colocados (pode ser row, row-reverse, column, column-reverse)
   * flex-wrap: define se os elementos ficarão em só uma fila ou em mais de uma(tem os valores wrap, wrap-reverse, nowrap).

   Exemplo: `flex-flow: row wrap;`
* flex: é uma propriedade de flex-item que engloba outras 3(flex: flex-grow flex-shrink flex-basis;) :
  * flex-grow: determina quanto esse flex-item crescerá em relação ao seus "elementos irmãos" com menores valores dessa propriedade(valores são 0,1,2,3,4, ...)
  * flex-shrink: o contrário do que o flex-grow faz(faz o elemento diminuir com base nos "elementos irmãos" com menores valores) 
  * flex-basis: dependendo se a flex-direction é row(ou row-reverse)/column(ou column-reverse), vai governar o width/height do flex-item

  {% hint style="info" %}
    OBS: é possível determinar somente a primeira propriedade, por exemplo: `flex: 1;`
  {% endhint %}

* justify-content/align-items: essas 2 propriedades de flexbox ajudam a ajustar o elemento no container, para auxiliar a colocá-los da forma que desejamos. Elas vão depender da flex-direction.
  Valores para justify-content(flex-direction da esquerda é row e o da direita é column):

  ![Flexbox justify-content row](/imagens/flexbox-row-justify-content.png) ![Flexbox justify-content column](/imagens/flexbox-column-justify-content.png)

  Valores para align-items(flex-direction da esquerda é row e o da direita é column):

  ![Flexbox align-items row](/imagens/flexbox-row-align-items.png) ![Flexbox align-items column](/imagens/flexbox-column-align-items.png)

* align-content: como as linhas(no caso de justify-content row) ou colunas(no caso de justify-content column) serão organizadas.

* align-self: valores do align-items; propriedade de flex-item, alinha apenas um item

* order: valores de 1,2,3, ...etc. propriedade de flex-item, ordena os items da forma em que o primeiro é o 1, o segundo é o 2, ...etc.

## Display Grid
Mais um valor possível para a propriedade display é grid(ou inline-grid), que forma um container(grid-container) com elementos em grade(grid-itens). Dessa forma, os elementos ficam organizados em linhas e colunas.
### Propriedades relacionadas
Algumas propriedades são utilizadas para ajustar a grid. Algumas delas são:
* Gap: é o conjunto de 2 outras propriedades, row-gap e column-gap, define o espaço entre as colunas e entre as fileiras. É uma propriedade para o container grid.
* Grid-template: uma propriedade para container, que é um shortcut para outras 3 propriedades:
  * Grid-template-rows: define o tamanho das linhas e quantas linhas serão formadas.
  Exemplo: `grid-template-rows: auto auto auto` significa que terão 3 linhas e o tamanho calculado das linhas será automático.
  * Grid-template-columns: define o tamanho das colunas e quantas colunas serão formadas.
  Exemplo: `grid-template-rows: 20% 20% 20%` significa que terão 3 colunas e o tamanho de cada linha será 20% do elemento.
  * Grid-template-areas: é uma propriedade que depende da nomeação de uma àrea usando uma propriedade no grid item, grid-area. Dessa forma, é possível definir um espaço mais(tanto para fileira quanto para coluna) para esse grid item ou vários definidos com o grid-area.
  Exemplo: `grid-template-areas: 'myArea myArea . . .' 'myArea myArea . . .';` significa que o grid item(definido dessa forma: `grid-area: myArea`) ocupará as primeiras 2 colunas e 2 fileiras.
* Grid-column/Grid-row/Grid-area: grid-area é a propriedade definida na anterior, porém ela pode ser usada como a junção entre grid-row e grid-column, os quais por sua vez representam 2 outras propriedades: grid-row-start/grid-column-start e grid-row-end/grid-column-end. Assim, essas propriedades, todas colocadas em grid-itens, determinam onde um elemento vai começar e onde vai terminar no grid, de forma que ele ocupe um espaço personalizado no grid.

## Propriedade Position
Essa propriedade determina como o elemento será disposto na tela em geral. Os valores possíveis são:
* static: é o valor padrão, significa um elemento não-posicionado, ou seja, ele será posto na forma padrão.
* fixed: o elemento não "descerá" com o resto da página.
* relative: o elemento fica normalmente na página, mas respeita algumas propriedades de posicionamento.
* absolute: o elemento é posicionado de acordo com algum elemento "pai" ou "avô" que seja posicionado(fixed, relative ou absolute).
* sticky: o elemento se comporta normalmente até o elemento ancestral mais próximo que tiver um scroll rolar até onde ele sairia da tela. Em vez disso, o elemento "gruda" no topo e continua sendo mostrado.

### Propriedades de posicionamento
São 4 propriedades(left, right, top, bottom) que governam onde os elementos posicionados(fixed, relative ou absolute) ficarão. Os valores possíveis são as unidades de medida, que determinam o "espaço" que o elemento vai ter desse lado. Por exemplo: `left: 10px` significa que o elemento ficará à 10 pixels da parte esquerda(seja da tela na `position:relative` e na `position:fixed` ou de algum container que seja posicionado e ancestral à esse elemento na `position:absolute`)

### Propriedade do z-index
Ela determina o grau de sobreposição entre elementos posicionados. Valores de 0,1,2,...etc que quanto maior o valor, mais em cima será colocado o elemento.

## Pseudo-classes
São classes que são definidas pelo próprio navegador e auxiliam a criar certas funcionalidades. A sintaxe é:
```css
outro-seletor:pseudo-class {
    propriedade: valor;
}
```
Algumas propriedades são:
* visited: serve para tags a(links), significa que o estilo será aplicado quando o link já estiver sido clicado anteriormente.
* hover: muda o estilo quando o mouse estiver sobre o elemento.
* active: muda o estilo quando o mouse clicar no elemento.
* nth-child: uma pseudo-classe para listas(é preciso selecionar os list itens). As opções são odd/even/3n/4n/...etc. Isso selecionará de acordo com a opção somente os itens nesse padrão e aplicará o estilo.

    Exemplo:
    ```HTML
    <ol>
        <li class="list-item">Ímpar</li>
        <li class="list-item">Par</li>
        <li class="list-item">Ímpar</li>
        <li class="list-item">Par</li>
    </ol>
    ```
    ```css
    .list-item:nth-child(even) {
        color: red;
    }
    ```
    ![nth-child even](/imagens/nth-child-even.png)