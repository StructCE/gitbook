# Finalização do Projeto
Quando um projeto está perto do término é importante seguir os passos abaixo.

## Checklist de Finalização de Projetos

### Jurídico
- Fazer documentação de termo de conclusão do projeto, como o modelo que está no google drive e coletar a assinatura do cliente, 
presidente e duas testemunhas. No momento utilizamos o ClickSign para esse processo.
- Coletar o NPS com o cliente, por meio do formulário que se encontra [em nosso drive](https://drive.google.com/drive/folders/160MBaimSfy-aAR3mpTl_EK54BaS0ry8C?usp=sharing).

#### Contrato de manutenção e hospedagem
Esse contrato normalmente é fechado para após o término de todos os projetos que efetuamos e trata-se dos serviços tanto de manutenção quanto de deploy do software. Geralmente tem duração de 12 meses e é cobrado um valor fixo mensal, que varia de acordo com o escopo do projeto:

Escopo do projeto     | Valor mensal
--------------------- | -------------------------------------------------------
Pequeno (até 5k)      | 50 reais
Médio (5k a 15k)      | 75 a 100 reais
Grande (15k a 25k)    | 100 a 150 reais
Muito Grande (até 5k) | Deve ser conversado com o cliente, a partir de 200 reais

{% hint style="info" %} 
Caso o cliente queira usar um servidor próprio, o valor do contrato é descontado em 20%. 
{% endhint %}

### Reunião de encerramento de projeto
Reunião final com o cliente, que deve acontecer apenas após todas as features estarem prontas e aprovadas pelo cliente. Apesar de ser bom pedir o feedback do cliente após a conclusão das funcionalidades, não é interessante que tenham infitas semanas de feedbacks, então é bom ter um limite bem definido, como um máximo de 1 alteração para cada feature.

Nessa reunião, devem estar presentes o gerente do projeto, o Product Owner (caso haja) e algum membro da diretoria de projetos para explicar sobre o deploy, hospedagem e domínio, além de ficar responsável por entrar em contato com algum piloto da diretoria de comercial para a confecção do [contrato de manutenção e hospedagem](#contrato-de-manutenção-e-hospedagem).

Ao longo da reunião, é importante apresentar o site completo com todas as funcionalidades, orientar o cliente para a compra de domínio e apresentar os [documentos jurídicos](#jurídico).

### Código
- Remover arquivos em branco, como helpers, arquivos de estilização e javascript que foram criados automaticamente.
- Revisar código em geral, procurando por falhas nas funcionalidades mais fundamentais do sistema.
- Mudar o timezone do rails para GMT-3 (Brasil).
- Limpar os warnings.
- Buscar fazer melhorias SEO (tornam o site mais seguro e aumentam a chance do google encontrá-lo)

### Deploy/Gestão
A equipe de projetos deve ficar responsável pelo deploy do site, que deve ser feito antes do prazo dado pelo cliente para colocar o site no ar.

- Definir uma pessoa para ficar a frente das futuras modificações de manutenção/garantia. Idealmente algum piloto que tenha participado do projeto, mas não necessariamente.
- Mudar todas as chaves de APIs para modo produção.
- Tenha preferência para todas as contas serem dos clientes, como Digital Ocean, Mailjet, GateWay de pagamento.
- **Domínio:** Deve ser comprado antes do deploy preferencialmente com uma semana de antecedência e é preciso que tenhamos acesso à ele.
- **Servidor:** Por padrão utilizamos o da Struct na Digital Ocean, mas cas o cliente queira podemos usar um servidor específico deles.

{% hint style="warning"%} 
Já tivemos alguns problemas com o Hostgator no passado e acabamos tendo que mudar de servidor para conseguir fazer o deploy, então se possível evite de usá-lo. Dê preferência a servidores com suporte ao docker.
{% endhint %}
