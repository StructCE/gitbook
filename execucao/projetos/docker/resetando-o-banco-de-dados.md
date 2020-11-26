# Resetando o Banco de Dados

Algumas vezes ao longo do projeto será necessário resetar o banco de dados do site em produção. Seja
por conta de alguma migração errada, ou então com o objetivo de deletar os registros por completo.

## Passo a passo
- Primeiramente entre no servidor da *Struct*
- Navegue até a pasta do `docker-compose.yml` do seu projeto
- Digite `docker-compose stop` para parar a excução do container
- Logo em seguida: `docker rm nomeprojeto_db_1` para remover o container do bd
- E depois `docker volume rm nomeprojeto_mariadb_data` para remover o volume do bd
- Para criar o banco de dados novo, digite: `docker-compose up -d` , porém será necessário rodar as migrações
- Então digite `docker exec -it nomeprojeto_nomeprojeto_1 /bin/sh` para navegar até o container que possui o rails
- E `rails db:setup` para rodar as migrações e o seed.rb
- Por último digite `docker-compose start` na pasta do seu `docker-compose.yml`, para reinciar os containers
- Pronto seu banco de dados está renovado
