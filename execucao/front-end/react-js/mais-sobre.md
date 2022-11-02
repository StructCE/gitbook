# O que realmente é?

Uma biblioteca que fornece `createElement()`, hooks e algumas utilidades a mais. Junto com algum plugin como Babel (ou typescript), converte JSX em `createElement()` e cria um elemento HTML quando chamado. Hooks são as maneiras de manejar o ciclo de vida e renderização do HTML. Ou seja, os hooks são úteis para que, por exemplo, quando uma variável do `useState` mude, o react sabe que o elemento deve ser renderizado novamente para mostrar as mudanças.

## Frameworks / Boilerplates

Não só react, nós usamos [create-react-app](https://create-react-app.dev/). Construído usando webpack, babel e react, vem com uma camada de abstração bem grossa, praticamente não necessitando de configuração.

Por mais que seja a maneira mais fácil de se iniciar no react, é altamente criticado por desenvolvedores por `facilitar más práticas` no gerenciamento e utilização de pacotes e `baixa configurabilidade` (o que dificulta manutenção e atualização). No contexto de nossa empresa, considerou-se que, apesar de seus problemas, vale a pena por ser a maneira mais `fácil de começar` um projeto com react.

## Que outras opções existem?

É sempre possível [configurar sua aplicação web do zero](https://thexcodes.com/crianto-uma-aplicacao-react-do-zero/), mas fica muito código e trabalho repetido entre projetos. Existem frameworks e boilerplates que já vem com a configuração inicial pronta pra isso:

- [Vite](https://vitejs.dev/)

  - Uma `ferramenta de construção` simples, que também inclui um `template` para react com ou sem typescript. Certamente a transição mais fácil de CRA (create-react-app).

  - Possui HMR (hot module reload) otimizado em comparação com CRA (ou seja, `fluxo de desenvolvimento mais rápido`) e usa Esbuild no lugar do Webpack (ou seja, faz `bundling muito mais rápido`). Além disso, possui muitas das features de CRA e possui bons plugins.

- [Next JS](https://nextjs.org/)

  - Um `framework` construído em cima do React e Nodejs, implementando `SSR` (server side render) já por padrão. É um ótimo framework tanto para desenvolvimento `front end` quanto para `full stack`.

  - SSR implica numa otimização do `carregamento inicial` das páginas (independe do pc lixo do usuário, somente do supercomputador usado como servidor), e de apresentação melhor de `metadados`.

{% hint style="info" %}

Vite e CRA são `SPA`s (single page applications) e `CSR` (client side rendered), isso `significa` que somente um HTML é dado para o cliente, e o resto do `HTML` é "`injetado`" pelo js `no próprio cliente`. Isso `implica` em `metadados` geralmente `ruins`, já que não se pode confiar no js para essa tarefa. Uma `solução` para esse problema é o `SSR`, já que o conteúdo da página é `injetado no servidor`, e só depois enviado para o cliente um HTML preenchido.

{% endhint %}

- [Remix](https://remix.run/)

  - Framework criado pela equipe responsável por React Router. Implementa SSR e o próprio react-router.

---

Menos úteis pra EJ:

- [create-t3-app](https://github.com/t3-oss/create-t3-app)

  - Alguns templates pra nextjs full stack, com configurações e integração de typescript entre algumas bibliotecas.

- [Bun](https://bun.sh/)

  - Será o novo node (aquele que roda código javascript fora do browser), e vai aumentar ainda mais a popularidade do SSR. Está sendo feito buscando compatibilidade máxima com aplicações já feitas. Ainda não está pronto pra produção, mas já tá sendo muito comentado.

{% hint style="info" %}

Fontes:
https://medium.com/codex/you-should-choose-vite-over-cra-for-react-apps-heres-why-47e2e7381d13

https://www.magnolia-cms.com/blog/spa-seo-mission-impossible.html

https://blog.betrybe.com/ferramentas/webpack-tudo-sobre/

https://webpack.js.org/

https://www.youtube.com/c/TheoBrowne1017

Além dos links já fornecidos na página.

{% endhint %}
