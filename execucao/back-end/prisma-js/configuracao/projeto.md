# Configuração do ambiente (para cada dev):

Criar um arquivo `.env` na raiz do projeto, seguindo o exemplo do `.env.example`

Substituindo os valores de acordo com o banco de dados local, basta rodar o comando:

```bash
yarn prisma:update
```

E agora o prisma já pode ser usado localmente.
