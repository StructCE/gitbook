# Exemplos de uso


## Next JS

```js
// src/pages/api/users/index.js

// Tenha certeza de que o caminho está correto
import { prisma } from "../../../prisma/client";

export default async function handler(req, res) => {
  // Encontra todos os usuários no banco de dados
  const users = await prisma.users.findMany();
  res.status(200).json({ users });
};
```

```js
// src/pages/api/users/[id].js
import { prisma } from "../../../prisma/client";

export default async function handler(req, res) => {
  // Pegando id da request:
    const { id } = req.query;

  // Encontra por propriedade que é única 
  const user = await prisma.users.findUnique({
    where: {
      id: req.query.id,
    },
  });

  res.status(200).json({ user });
};
```

Caso o usuário tenha uma relação com outra tabela que desejamos mostrar, podemos usar o `include`. Exemplo sendo que usuário tem uma relação com `posts`:

```js
// src/pages/api/users/[id].js
import { prisma } from "../../../prisma/client";

export default async (req, res) => {
  // Pegando id da request:
    const { id } = req.query;

  // Encontra por propriedade que é única 
  const user = await prisma.users.findUnique({
    where: {
      id: id,
    },
    include: {
      posts: true,
    },
  });

  res.status(200).json({ user });
};
```


```js
// src/pages/api/users/create.js
import { prisma } from "../../../prisma/client";

export default async function handler(req, res) => {
  // Pegando dados da request:
  const { name, email } = req.body;

  const user = await prisma.users.create({
    data: {
      name,
      email, // equivalente a 'email: email'
    },
  });

  res.status(200).json({ user });
};
```


