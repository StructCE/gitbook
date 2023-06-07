# Rotas no Next JS

Rotas no Next.js são de fato endpoints criados para serem acessados via HTTP. Para criar uma rota, basta criar um arquivo com o nome da rota dentro da pasta `pages`. Next cuida do resto.

Para que a mágica do Next funcione, é necessário exportar como default a função que será executada quando a rota for acessada (ou seja,a página ou a api req handler).

## Páginas

Para criar uma rota chamada `about`, basta criar um arquivo chamado `about.js`, ou `about/index.js` dentro da pasta `pages`. Esse arquivo será acessado via `http://localhost:3000/about`.

Para criar uma rota com parâmetros, basta colocar usar colchetes ao redor desse parâmetro. Por exemplo, para criar uma rota chamada `/user/:id`, com parâmetro `id`, basta criar uma pasta e arquivo formando a rota `pages/user/[id].js`. Esse arquivo será acessado via `http://localhost:3000/user/1`.

Para criar uma rota com múltiplos parâmetros, podemos criar pasta e arquivo `users/[id]-[name].js`, ou então `users/[id]/[name].js`, como sempre dentro da pasta `pages`. Esse arquivo será acessado via `http://localhost:3000/user/1-joao` no primeiro caso, e via `http://localhost:300/user/1/joao`.

Lembre que essas rotas são apenas endpoints, e não páginas. Para criar páginas, é necessário criar um componente React na rota e exportá-lo como default.

### Exemplos

Podemos usar o hook useRouter dentro da página caso queremos acessar os parâmetros da rota pela página.

```jsx
// src/pages/users/[id].js

import { useRouter } from "next/router";

export default function User() {
  const router = useRouter();
  const { id } = router.query;

  return <h1>User {id}</h1>;
}
```

```jsx
// src/pages/users/[id]/posts/[postId].js

import { useRouter } from "next/router";

export default function Post() {
  const router = useRouter();
  const { id, postId } = router.query;

  return (
    <>
      <h1>User {id}</h1>
      <h2>Post {postId}</h2>
    </>
  );
}
```

Podemos acessar os parâmetros da rota pelo contexto, caso queremos acessar os parâmetros da rota fora da página.

```jsx
// src/pages/users/[id].js

export default function User({ id }) {
  return <h1>User {id}</h1>;
}

export async function getServerSideProps(context) {
  const { id } = context.params;
  // podemos fazer uma chamada para a api agora, com o id da rota
  // const data = await api.get(`/users/${id}`)

  return {
    props: {
      id,
    },
  };
}
```

## API

Para criar uma rota de api, basta criar um arquivo dentro da pasta `pages/api`. Esse arquivo será acessado via `http://localhost:3000/api/`. O arquivo deve exportar default uma função que será executada quando a rota for acessada.

De resto, o roteamento de api é igual ao de páginas, com a diferença que a função exportada default recebe como parâmetro o objeto `req` e `res` do node, e deve responder à request a partir do `res`. Caso não seja feito isso, a request ficará pendente. Além disso, pode-se terminar a request com `res.end()`. Caso isso não seja feito, a request responderá com o definido até a função terminar sua execução pelo objeto `res`.

### Exemplos

Exemplo padrão de rota de api.

```jsx
// src/pages/api/hello.js

export default function handler(req, res) {
  res.status(200).json({ name: "John Doe" });
}
```

Exemplo usando parâmetros

```jsx
// src/pages/api/users/[id].js

export default function handler(req, res) {
  const { id } = req.query;
  res.status(200).json({ id, name: "John Doe" });
}
```
