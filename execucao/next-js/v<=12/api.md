# Next API

O Next JS usa api padrão do Node.js, então você pode usar qualquer biblioteca que você quiser. O Next JS também tem uma API própria que pode ser usada para algumas coisas, como rotas, renderização do lado do servidor e renderização estática.

```jsx
// src/pages/api/users/[id].js

export default function handler(req, res) {
  const { id } = req.query;
  prisma.users.findUnique({ where: { id } }).then((user) => {
    res.status(200).json(user);
  });
}
```

Exemplo usando o prisma para acessar o banco de dados.

```jsx
// src/pages/api/users.js

export default function handler(req, res) {
  prisma.users.findMany().then((users) => {
    res.status(200).json(users);
  });
}
```

Exemplo usando múltiplos parâmetros

```jsx
// src/pages/api/users/[id]/posts/[postId].js

export default function handler(req, res) {
  const { id, postId } = req.query;
  prisma.posts
    .findUnique({
      where: { id: postId }, // encontrando o post pelo seu id
      include: { user: true }, // incluindo o usuário que criou o post
    })
    .then((post) => {
      res.status(200).json(post);
    });
}
```

Exemplo usando o método POST na mesma rota, autenticando com headers antes

```jsx
// src/pages/api/users.js

export default function handler(req, res) {
  if (req.method === "POST") {
    handlePost(req, res);
  } else {
    // handle outros métodos
    prisma.users.findMany().then((users) => {
      res.status(200).json(users);
    });
  }
}

function handlePost(req, res) {
    // get auth header
    const authToken = req.headers["X-Auth-Token"];
    const authEmail = req.headers["X-Auth-Email"];

    // check if auth header is valid
    const userRequesting = await prisma.users.findUnique({
      where: { email: authEmail },
    });

    // guard clause para caso o usuário não tenha permissão
    if (!userRequesting || !userRequesting.authentication_token === authToken) {
      res.status(403).json({ error: "Forbidden" });
      // caso seja inválido, não proceder com a função, retornar
      return;
    }

    const { name, email, password } = req.body;

    // validar corpo da request para criar o usuário
    const {isInvalid, errors} = validateUser({ name, email, password });

    if (isInvalid) {
        res.status(422).json({ errors });
        // caso seja inválido, não proceder com a função, retornar
        return;
    }

    // create user
    prisma.users
        .create({
            data: {name, email, password}
        })
        .then((user) => {
            res.status(200).json(user);
        })
        .catch((err) => {
            res.status(422).json(err);
        });
}
```
