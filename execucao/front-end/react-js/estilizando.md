# Styled components

Na Struct, usamos a biblioteca `styled-components` para estilizar nossos componentes.
Para instalar, basta rodar no projeto:

```bash
yarn add styled-components
```

{% hint style="info" %}

Como material de referência, podendo até editar: https://codesandbox.io/s/styled-components-demo-5ir4oo

{% endhint %}

O styled-components nos fornece algumas ferramentas para criar componentes estilizados. Se o componente for uma simples tag HTML estilizada, podemos colocar o estilo diretamente no `index.js` do componente. Quando mais complexo, separamos os estilos no `styles.js`, e usamos eles no index.

```js
// src/components/button/index.js
import styled from "styled-components";

const Button = styled.button`
	background-color: red;
	font-size: 1.75rem;
`;
```

{% hint style="info" %}

Para adicionar sintaxe de css e aparência mais bonita, ao invés de ficar o laranja de string, adicionar alguma extensão. No vscode, existe a extensão "styled-components" para tal.

{% endhint %}

Podemos também passar propriedades para customizar o estilo. Por exemplo, se o botão na verdade for:

```js
const Button = styled.button`
	background-color: ${(props) => props.backgroundColor};
	font-size: 1.75rem;
`;
```

{% hint style="info" %}

É boa prática deixar algum valor padrão a ser utilizado caso não seja passado a prop:

`${(props) => props.backgroundColor || "red"}`

{% endhint %}

Podemos chamar um botão da cor que quisermos, mantendo os outros estilos:

```js
<Button backgroundColor="cyan">Clique aqui</Button>
```

O bloco acima retorna um botão com cor de fundo "cyan".

Saiba mais em:
https://styled-components.com/docs/basics#getting-started
