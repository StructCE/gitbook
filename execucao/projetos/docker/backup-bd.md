# Backup Banco de dados
É sempre importante ter alguns backups dos banco de dados em produção para caso aconteca qualquer tragédia,
ou então caso você precise testar modificaçes no seu computador com o banco de dados em produção

## Passo a passo
- Primeiramente entre no servidor da Struct
- Digite: ```docker exec <CONTAINER> /usr/bin/mysqldump -u root —password=<PASSWORD> <DATABASE> > nomedoarquivo.sql ```
- Use ```docker ps```, para localizar seu container e olhe o docker-compose para localizar a senha e o nome do database
- Com esse comando será criado um arquivo nomedoarquivo.sql na pasta atual que você rodou o comando no servidor
, que guarda toda a informação do seu banco de dado
- Pronto você já tem o backup, mas como eu passo para o meu pc local? Basta digitar o comando 
```scp root@struct.unb.br:<CAMINHO DO ARQUIVO> . ```, no seu terminal, que ele salvará o arquivo na pasta atual do terminal
- E para substituir o banco de dados local pelo backup: ```mysql -u root --password-<PASSWORD> databasename < file.sql```
