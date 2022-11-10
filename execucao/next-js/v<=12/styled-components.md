# Usando styled-components com Next.js

## Possíveis problemas

Para usarmos o styled-components no Next.js, precisamos mudar configurações. Caso contrário, poderão ocorrer _hydration errors_, e comportamento estranho dos estilos.

## Configuração

Para isso, vamos substituir o compilador padrão do next por um do babel, e adicionar o styled-components como plugin.

Primeiro, vamos instalar as dependências necessárias:

```bash
yarn add -D babel-plugin-styled-components
yarn add styled-components
```

Agora, vamos criar um arquivo de configuração do babel, chamado `.babelrc`, na raiz do projeto, e adicionar o seguinte conteúdo:

```js
// .babelrc
{
  "presets": ["next/babel"],
  "plugins": [
    [
      "styled-components",
      {
        "ssr": true,
        "displayName": true,
        "preprocess": false
      }
    ]
  ]
}

```

Pronto! Agora, podemos usar o styled-components no Next.js.
{% hint style="info" %} OBS: Seria melhor nem usar styled-components... {% endhint %}
