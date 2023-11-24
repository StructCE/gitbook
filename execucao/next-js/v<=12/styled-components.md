# Usando styled-components com Next.js

## Possíveis problemas

Para usarmos o styled-components no Next.js, precisamos mudar configurações. Caso contrário, poderão ocorrer _hydration errors_, e comportamento estranho dos estilos.

## Configuração

Basta alterar o arquivo `next.config.js`, alterando `nextConfig.compiler.styledComponents = true`:


```js
// next.config.js
/** @type {import('next').NextConfig} */
const nextConfig = {
  // outras opções
  compiler: {
    // possivelmente outras opções
    // adicionar:
    styledComponents: true,
  },
};

module.exports = nextConfig;

```

Pronto! Agora, podemos usar o styled-components no Next.js.
{% hint style="info" %} OBS: Seria melhor nem usar styled-components... {% endhint %}
