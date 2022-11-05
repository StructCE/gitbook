# SSR, ISR e SG, mas como?

O next permite fazer páginas com SSR, ISR e SG, mas como que usamos isso?

## ATENÇÃO:

No ambiente de `desenvolvimento` local, `NÃO SERÃO PERCEBIDAS DIFERENÇAS` direito entre esses padrões!! Por usar React Fast Refresh, toda hora que uma alteração ocorrer nos arquivos de desenvolvimento, acontecerá o equivalente a tirar o servidor do ar e levantá-lo novamente. Isso dificulta observar o comportamento que ocorrerá na aplicação com o servidor no ar.

Além disso, esses `padrões` de renderização são `somente` para `páginas`, em 'pages/'. Os `componentes` devem ser desenvolvidos como em React normal, em `outro diretório`. Isso também implica que, para se aproveitar dos padrões do Next, é necessário saber e `requisitar` os `dados` que os `componentes` de uma página necessitam a `nível` de `página`, e não a nível de `componente`.

## SG

Por padrão, uma página no Next será compilada para um _asset_ estático no momento de _build_. Caso queira fazer uma chamada à api no momento de build, pode ser utilizada a função `getStaticProps`.

### Exemplo:

```jsx
// src/pages/index.js

import { useState } from "react";

// Note que  é  necessário fazer um export default da página
export default function Home() {
  const [todos, setTodos] = useState(null);

  async function getData() {
    const response = await fetch(
      "https://jsonplaceholder.typicode.com/todos/1"
    );
    const todos = await response.json();
    setTodos(todos);
  }

  return (
    <div>
      <h1>SG</h1>
      <button onClick={getData}>Get Data</button>
      {todos && <pre>{JSON.stringify(todos, null, 2)}</pre>}
    </div>
  );
}
```

Essa página seria acessada pela url `http://localhost:3000/`.

### Exemplo com getStaticProps:

```jsx
// src/pages/wGetStaticProps.js

import { useState } from "react";

// Note que  é  necessário fazer um export default da página
export default function wGetStaticProps({ initialTodos }) {
  const [todos, setTodos] = useState(initialTodos);

  async function getData() {
    const response = await fetch(
      "https://jsonplaceholder.typicode.com/todos/1"
    );
    const todos = await response.json();
    setTodos(todos);
  }

  return (
    <div>
      <h1>SG</h1>
      <button onClick={getData}>Get Data</button>
      {todos && <pre>{JSON.stringify(todos, null, 2)}</pre>}
    </div>
  );
}

// getStaticProps é uma função que é executada no momento de build
// e que retorna um objeto com as props que serão passadas para a página
export async function getStaticProps() {
  const response = await fetch("https://jsonplaceholder.typicode.com/todos/1");
  const todos = await response.json();

  return {
    props: {
      initialTodos: todos,
    },
  };
}
```

Essa página seria acessada pela url `http://localhost:3000/wGetStaticProps`. A diferença entre essa página e a primeira é que essa faz uma chamada à api no momento de build, preenchendo as props da página com a resposta.

Essas páginas são renderizadas na build do app, e _assets_ estáticos são gerados, incluindo seu HTML e JS. Quando o usuário acessar a página, o HTML e JS serão enviados como estão, e o usuário não precisará esperar o servidor renderizar a página ou fazer qualquer processamento.

## ISR

Para transformar uma página de SG para ISR, existem algumas maneiras. Uma delas é usar a função `getStaticProps` e passar um parâmetro `revalidate` para ela. Esse parâmetro é um número que representa o tempo em segundos que o Next deve esperar para revalidar a página. Por exemplo, se o parâmetro for 10, a página será revalidada a cada 10 segundos.

### Exemplo com revalidação a cada 10 segundos:

```jsx
// src/pages/wISR/index.js.js

// export default Pagina () {...}

export async function getStaticProps() {
  const response = await fetch("https://jsonplaceholder.typicode.com/todos/1");
  const todos = await response.json();

  return {
    props: {
      initialTodos: todos,
    },
    revalidate: 10, // Revalida a página a cada 10 segundos
  };
}
```

Página acima acessada pela url `http://localhost:3000/wISR`.

Outra maneira de transformar uma página de SG para ISR é usando a função `getStaticPaths`. Essa função é executada no momento de build e deve retornar um objeto com um parâmetro `paths`, um array de objetos com `params`. Cada objeto dentro de `paths` representa uma página/url que será gerada no momento de build.

### Exemplo de getStaticPaths:

```jsx
// src/pages/wISR/[id].js

// export default Pagina () {...}

export async function getStaticProps(context) {
  // context é um objeto que sempre é passado para essas funções,
  // contendo informações sobre a requisição

  // pegando id da rota do next
  const { id } = context.params;

  const response = await fetch(
    `https://jsonplaceholder.typicode.com/todos/${id}`
  );

  const todos = await response.json();

  return {
    props: {
      initialTodos: todos,
    },
  };
}

export async function getStaticPaths() {
  return {
    paths: [
      { params: { id: "1" } },
      { params: { id: "2" } },
      { params: { id: "3" } },
    ],
    fallback: "blocking",
  };
}
```

O parâmetro `params` é um objeto com os parâmetros que serão passados para a página. De acordo com o exemplo exemplo, se a página for acessada pela url `http://localhost:3000/wISR/1`, o objeto `params` deve ser `{ id: 1 }`. O Next irá gerar uma página para cada objeto dentro de `paths`.

Além disso, o fallback determina o comportamento que o Next deve ter quando uma página não estiver gerada ainda.

- Se o fallback for `false`, o Next irá retornar um erro 404.
- Se o fallback for `true`, não lembro o que acontece. Pesquisa aí e adiciona nessa documentação, caro leitor.
- Se o fallback for `blocking`, o Next irá gerar a página no momento da requisição, e irá bloquear a requisição até que a página seja gerada (que é o mesmo comportamento que no SSR).

## SSR

Para fazer SSR, é necessário que a página tenha a função `getServerSideProps` exportada. Essa função é executada no servidor no momento da request, e o retorno dela é passado para a página como `props`.

Usamos SSR quando precisamos de dados que não podem ser gerados no momento de build, ou quando queremos sempre o conteúdo mais atualizado possível.

```jsx
// src/pages/wSSR/index.js
import { api } from "../../services/api";

export default function Page({ products }) {
  return (
    <div>
      <h1>SSR</h1>
      <ul>
        {products.map((product) => (
          <li key={product.id}>
            <h2>{product.name}</h2>
            <p>{product.description}</p>
          </li>
        ))}
      </ul>
    </div>
  );
}

export async function getServerSideProps(ctx) {
  // get request info from context
  const { req } = ctx;

  // get req headers
  const { headers } = req;

  // get auth header
  const authToken = headers["x-auth-token"];

  // get products
  api.get("/products", {
    headers: {
      "x-auth-token": authToken,
    },
  });

  return {
    props: {
      products: products,
    },
  };
}
```
