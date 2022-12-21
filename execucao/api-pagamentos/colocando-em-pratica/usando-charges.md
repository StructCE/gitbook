O [Pagar.me](http://Pagar.me) não disponibiliza funcionalidade de parcelamento de boleto. Assim, caso seja necessária a geração de múltiplos boletos para o mesmo pedido, precisaremos fazer algumas adaptações que tornarão isso possível.

No exemplo, criaremos um pedido que será pago por 2 boletos: o primeiro será gerado automaticamente com a criação da Order, e o segundo será gerado utilizando o método create_boleto_charge. 

Assim, precisamos fazer algumas alterações no processo:

- Criaremos a Order no modo ‘aberto’ (closed: false). Assim, temos a possiblidade de incluir Charges adicionais.
- Utilizaremos a response da criação da Order para capturar o order_id. Assim, nosso método de inclusão de boletos adicionais saberá a qual Order adicionar Charges.
- Fecharemos a Order para impedir a adição de novas Charges por meio do método close_order.

### create_boleto_order

**app/services/payment/proxy.rb**

```ruby
def create_boleto_order(pedido)

			# Estruturando o request
      order_request = {
        code: pedido.id,
        items: pedido.items,
        customer: pedido.customer,
        payments: [
          {
            payment_method: 'boleto',
            boleto: {
              bank: '273', # Banco do Boleto a ser gerado
              instructions: "Exemplo",
              due_at: *vencimento_boleto_1,*
              document_number: nil         
            }
          }
        ],
        closed: false, # Criando Order aberta
      }

			# Coletando response da criação da Order
      order_result = @@orders_controller.create_order(order_request)

			# Coletando o id da Order criada pelo Pagar.me
      order_id = order_result.id
			
			# Adicionando boleto a Order por meio do order_id
      charge_result = create_boleto_charge(
        order_id,
        pedido,
        *vencimento_boleto_2*
      )

			# Fechando a Order
			close_package_result = close_order(order_id)
	end
end
```

### create_boleto_charge

**app/services/payment/proxy.rb**

```ruby
def create_boleto_charge(order_id, pedido, vencimento_boleto)
      payment = {
          payment_method: pedido.payment_method,
          boleto: {
            instructions: "Exemplo",
            due_at: pedido.vencimento,
            document_number: nil,
            type: "DM"            
          }
      }

      charge_request = PagarmeCoreApi::CreateChargeRequest.new(
        code = pedido.id,
        amount = pedido.valor,
        customer_id = nil,
        customer = package.customer,
        payment = payment,
        metadata = nil,
        antifraud = nil,
        pedido.order_id,
        due_at = pedido.vencimento
      )

      charge_result = @@charges_controller.create_charge(charge_request, idempotency_key = nil)
    end
```

### close_order

**app/services/payment/proxy.rb**

```ruby
def close_order(order_id)
      close_order_request = PagarmeCoreApi::UpdateOrderStatusRequest.new
      result = @@orders_controller.close_order(order_id, close_order_request, idempotency_key = nil)
end
```

### Considerações

Note que para parcelar um boleto por N vezes, precisaremos criar a order (que carrega o boleto inicial) e chamar o método de criação de charge N-1 vezes, o que significa o provável uso de um loop. Cada loop realizará uma chamada a API que demora alguns segundos - e quanto mais parcelas, maior o tempo de execução total. Os maiores parcelamentos que implementamos - de 24x, ou 1 chamada de criação de Order e 23 chamadas de criação de Charge - fizeram com que todo o processo de pagamento demorasse mais que um minuto! Tanta demora, claro, é longe do ideal. Mas é algo que, por enquanto, não há pra onde fugir com o [Pagar.me](http://Pagar.me) já que temos que realizar uma chamada individual para cada boleto.

A falta de um método automatizado para a criação de vários boletos também significa que o cálculo das datas de vencimento de cada um desses boletos fica totalmente por nossa conta, e trabalhar com datas é laborioso, delicado, e um tanto chato. 

Vamos escolher o dia 25 de todo mês como o dia do vencimento para os boletos. Acompanhe os comentários do código de acordo com cada operação.

Caso a data de vencimento caia em um final de semana ou feriado, não se preocupe. O pagamento é quitado no próximo dia útil por lei.

```ruby
# Definindo um dia de vencimento fixo para os Boletos
payment_day = 25

base = Time.now

# Definindo margem de 5 dias para pagamento do boleto
base += 432000 # 5 dias em segundos
first_month = base.month
first_year = base.year

# Checando se o dia de pagamento já terá passado daqui a 5 dias.
# Se sim, mandamos o primeiro pagamento só pro próximo mês.
if base.day > payment_day
	# Se já é dezembro, definimos o pagamento para janeiro e incrementamos o ano
  if first_month != 12
    first_month += 1
  else
    first_month = 1
    first_year += 1
  end
end

=begin 
Definindo a data de vencimento do primeiro boleto.
Em alguns lugares da Dashboard do Pagarme, o fuso horário não é corretamente
aplicado à data de vencimento. Como não possuem previsão de fix, definimos
o horário como 20:59 para garantir que a falta do fuso horário não alterará
o dia do pagamento.
=end
first_boleto_due_at = Time.new(
  first_year,
  first_month,
  payment_day,
  20,
  59,
  00,
  "-03:00"
)

# Montando o request da Order com o vencimento do Primeiro Boleto
order_request = {
	...
	due_at: first_boleto_due_at,
  ...
}

order_result = @@orders_controller.create_order(order_request)
order_id = order_result.id

base_year = first_year
base_month = first_month
y = 0

# Criação de 23 cobranças adicionais
(1..23).each do |m|

  boleto_month = base_month + m - (12*y)
  
  if (boleto_month) > 12
    y += 1
    boleto_month = base_month + m - (12*y)
  end

  boleto_year = base_year + y

	boleto_due_at = Time.new(
	          boleto_year,
	          boleto_month,
	          payment_day,
	          20,
	          59,
	          00,
	          "-03:00"
	        )
	#Chamada para criação do boleto
  charge_result = create_boleto_charge(
    order_id,
    pedido,
    boleto_due_at
  )

end

close_package_result = close_order(order_id)
```