Para invocar os métodos de serviço, iremos acessar nosso módulo de pagamentos por meio de um método em model. Para uma hipotética model Pedido, usada para registrar dados acerca de uma compra em e-commerce, criaremos uma instância equivalente na API do [Pagar.me](http://Pagar.me) de acordo com o exemplo a seguir:

**app/models/pedido.rb** 

```ruby
class Pedido < ApplicationRecord

def create_pedido_proxy(payment_method, card_hash=nil)
  
		# Acesso a todos os métodos dentro da classe Proxy do módulo Payment.
		payment_proxy = Payment::Proxy.new 
   
		if (payment_method == 'credit_card' && card_hash)
	    pedido_proxy = payment_proxy.create_credit_card_order(
	      self,
	      card_hash
	  )
		elsif payment_method == 'boleto'

      pedido_proxy = payment_proxy.create_boleto_order(
        self
     )
	
    return pedido_proxy

  end
```

**app/services/payment/proxy.rb**

```ruby
module Payment
  class Proxy

		def create_boleto_order(package, bank)

      order_request = {
        code: pedido.id,
        items: pedido.items,
        customer: pedido.customer,
        payments: [
          {
            payment_method: 'credit_card',
            credit_card: {
              installments: pedido.installments,
              statement_descriptor: "Pedido",
              card_id: card_hash
            }
          }
        ]
      }
      
      order_result = @@orders_controller.create_order(order_request)
	end
end
```

##