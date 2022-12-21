No caso de pagamento por cartão de crédito, o [Pagar.me](http://Pagar.me) aborda algumas formas de implementação diferentes, algumas mais completas do que outras. Consulte a documentação e avalie as opções disponíveis. Referindo à seção de Melhorias Futuras, considere a utilização do Checkout Pagar.me.

A implementação a ser tratada é a mais *barebones* possível: criaremos um token do cartão. Vamos realizar uma chamada direta à API do [Pagar.me](http://Pagar.me) com os dados do cartão a partir do front-end, e receberemos um token expirável e de uso único que representará aquele cartão na transação subsequente. Aqui, o chamaremos de card_hash e o atrelaremos à criação do pedido na API Rails. Dessa forma, as funções de pagamento do *proxy* terão acesso ao cartão para efetuar as transações por meio do objeto pedido da API Rails. 

Seguindo o código abaixo como exemplo, iremos realizar uma requisição para a rota disponibilizada na [Referência](https://docs.pagar.me/reference/criar-token-cartão-1). Junto a ela, mandaremos alguns parâmetros:

- appId - string passada como parâmetro de Query (definido após a ? na rota)
- type - string definida no corpo da requisição
- card - objeto que encapsula os dados do cartão

Após realizada a requisição, basta acessarmos o campo [data.id](http://data.id) da resposta para obter o token do cartão, ou card_hash, e armazená-lo no objeto pedido para uso nas transações.

**Importantíssimo: nunca mande dados de pagamento abertos/sensíveis para a API Rails!** O método do token vem justamente como alternativa mais segura para trafegar o cartão pelo nosso back-end. Abaixo, segue código exemplo de implementação da chamada no nosso front-end. 

Note a presença dos headers no envio da requisição - a não inclusão de algum deles provavelmente resultará em um bloqueio de CORS! Certifique-se que os campos de números (number, exp_month e exp_year) sejam convertidos para o tipo correto - use Number() para tal- e que não carregam caracteres da formatação - use replace() manipular a string.

```jsx
	const [cvv, setCvv] = useState('');
  const [number, setNumber] = useState('');
  const [expDate, setExpDate] = useState('');
  const [name, setName] = useState('');
  let history = useNavigate();

  const handleSubmit = async (e) => {
    e.preventDefault()
    try {
        const response = await axios.post("https://api.pagar.me/core/v5/tokens?appId=<chave_publica>", {
            type: 'card',
            card: {
                number: Number(number.replace(/\D/g,'')),
                holder_name: name,
                exp_month: Number(expDate[0] + expDate[1]),
                exp_year: Number(expDate[3] + expDate[4]),
                cvv
            }
        }, {
            headers: {
                'content-type': 'application/json',
                accept: 'application/json'
            }
        });
        setCardHash(response.data.id)
        alert("Cartão confirmado com sucesso!")
    } catch (error) {
        alert('Erro processamento do cartão. Tente novamente');
    }

      if (name === "" || number === "" || expDate === "" || cvv === "") {
          alert("Preencha todos os campos para efetuar sua compra!")
          return
      }
  }
```

##