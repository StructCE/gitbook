# O que pode dar muito errado:

Acessar o banco de dados em dois apps diferentes. Por exemplo, se colocarmos validações somente no rails, e não no prisma, podemos ter problemas de segurança, pois o prisma não vai validar nada. Se fizermos nos dois, podemos ter problemas de duplicação de código, dificuldade de manutenção e mais bugs. Sendo assim, o ideal é deixar a responsabilidade de escrever no banco de dados para um único app.
