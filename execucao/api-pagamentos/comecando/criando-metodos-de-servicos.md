Como um primeiro passo, realize uma análise sobre os requisitos a serem cumpridos pelo sistema:

- Qual é a principal modalidade de pagamento? (*e.g.* venda de produtos, serviço de assinatura*)*
- Quais meios de pagamentos estarão disponíveis? (*e.g.* cartão de crédito, boleto, pix)
- O pagamento deverá ser dividido entre mais de uma entidade? (*e.g.* split de pagamentos)

Após feita a análise, acesse a documentação da [SDK em Ruby do Pagar.me](https://github.com/pagarme/pagarme-core-api-ruby). A SDK fornece uma lista de controllers e seus respectivos métodos disponíveis na API Pagar.me - que não devem ser confundidos com controllers e métodos da API Rails. 

Com base na análise de requisitos do sistema, iremos declarar todas as controllers e métodos da API Pagar.me que se enquadram nos casos de uso do sistema. 

Em nosso exemplo ilustrativo, nossos requisitos são:

- Criar um pedido. 
- Obter informações sobre o pedido.

Para isso, nos apoiaremos no objeto Pedido da API Rails, e de um objeto da API [Pagar.me](http://Pagar.me) que mais se encaixe nos requisitos. Nesse caso, se trata do objeto Order. Vamos declarar sua controller:

**app/services/payment/proxy.rb**

```ruby
module Payment
  class Proxy

	client = PagarmeCoreApi::PagarmeCoreApiClient.new(
	  basic_auth_user_name: basic_auth_user_name,
	  basic_auth_password: basic_auth_password
	)

	@@orders_controller = client.orders

	end
end
```