# Configuração no projeto (uma única vez):

{% hint style="info" %}
Trecho voltado à gerência
{% endhint %}

Adicionar o prisma CLI (Command Line Interface) ao projeto como dependência de desenvolvimento:

```bash
yarn add -D prisma
```

Então inicializar o prisma:

```bash
yarn prisma init --datasource-provider postgresql
```

Adicione `.env` ao `.gitignore`

#### Integrando com banco de dados externo (e.g. do rails):

{% hint style="info" %}
O prisma pode cuidar da criação do banco de dados, mas por enquanto vamos usar o banco de dados do rails. Para isso, precisamos configurar o prisma para usar um banco de dados externo.
{% endhint %}

Adicionar ao arquivo `.env.example` (criá-lo caso não exista) o seguinte conteúdo:

```text
# Variáveis de ambiente para o prisma:

DATABASE_URL="postgresql://user:password@localhost:5432/<database>"
# DATABASE_URL="postgresql://<db_user>:<db_password>@localhost:5432/<db_name>?schema=public"
```

Substitua acima o <db_name> pelo nome do banco de dados. O rails por padrão pega o nome do projeto e coloca adiciona um pósfixo `_development`. Então, se o nome do projeto for `projeto-api`, o banco de dados de desenvolvimento será `Projeto_api_development`, e o arquivo ficaria assim:

```text
DATABASE_URL="postgresql://<user>:<password>@localhost:5432/Projeto_api_development"
```


{% hint style="info" %}

A url de conexão com o banco de dados tem o seguinte padrão, caso seja necessário mudar alguma parte:

```text
postgresql://<user>:<password>@<host>:<port>/<database>?schema=<schema>
```

#### Criando o client do prisma:

Adicionar isso, adicionar aos script em `package.json`:

```json
"scripts": {
    // ...scripts anteriores
    "prisma:update": "yarn prisma db pull && yarn prisma generate",
},
```

Então, na pasta `prisma`, criar um arquivo chamado client.js, com o seguinte conteúdo:

```js
import { PrismaClient } from "@prisma/client";

// Permite que BigInt seja serializável para JSON, e funcione corretamente
// caso existam tais campos no banco de dados
// O rails por padrão usa BigInt para os ids
BigInt.prototype.toJSON = function () {
  return this.toString();
};

export const prisma = new PrismaClient({
  log: ['query', 'info', 'warn', 'error'],
});
```

