Há duas maneiras de se realizar chamadas a API e elas se diferenciam somente pelo jeito que construimos o nosso request. 

## Opção 1
 
**app/services/payment/proxy.rb**

```ruby
order_request = PagarmeCoreApi::CreateOrderRequest.new(param1, param2...)
@@orders_controller.create_order(order_request)
```

## Opção 2

**app/services/payment/proxy.rb**

```ruby
module Payment
  class Proxy

		def create_credit_card_order(pedido, card_hash)

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

A Opção 1 utiliza um método de construção específico para cada tipo de request, que é disponibilizado pela SDK do Pagar.me. Podemos acessá-los por meio do módulo PagarmeCoreApi, e passar os parâmetros diretamente para o método. O order_request resultante será um JSON estruturado e pronto para comunicar com a API.

Entretanto, o comportamento dos métodos construtores não é bem descrito pelas documentações. Pelas nossas experiências prévias, a ordem dos parâmetros nem sempre é óbvia, principalmente lidando com parâmetros opcionais (como um objeto de Split de Pagamentos). Sempre podemos investigar o [código desses métodos](https://github.com/pagarme/pagarme-core-api-ruby/tree/main/lib/pagarme_core_api/models) para descobrir a ordem correta, mas no fim das contas, isso pode acabar de tornando laborioso.

A Opção 2, por sua vez, é construir o request manualmente em um formato JSON. Como o JSON segue a [estrutura proposta na documentação](https://docs.pagar.me/reference/criar-pedido-2) (ou pelo menos espera-se que siga), criar o request manualmente pode acabar se tornando mais simples. Seguir essa opção não elimina por completo a tentativa e erro, mas pode fornecer uma clareza maior no código quanto à estrutura do objeto.

Ambas as opções são válidas. Em um mundo ideal, é interessante que o código se atenha a uma dessas opções por fins de previsibilidade -  mas também sabemos que o mundo do software nem sempre é o ideal.

Teste ambas as opções e decida qual se adequa melhor ao método sendo empregado, levando em consideração a quantidade de parâmetros e a complexidade da estrutura. Em tese, a Opção 1 é mais elegante e deve ser priorizada. Mas caso esteja muito difícil descobrir a ordenação dos parâmetros, não se impeça se utilizar a Opção 2, que deixa sua estrutura clara e funciona igualmente bem.

Durante os testes, pode haver confusão quanto ao tipo do erro ocorrido. **Não confunda erro de requisição com erro de parâmetro!** Muitas vezes, a estrutura estará correta e seu impeditivo será um parâmetro inválido. Refira-se à seção ‘Reconhecendo Erros’ desta documentação, ou acesse a [referência oficial sobre Erros](https://docs.pagar.me/reference/erros-1).

Após estruturado o request, basta invocarmos o método correspondente da controller em questão - é por meio desse método que realizamos a conexão externa de fato com a API. Consulte a SDK para saber quais métodos são suportados por cada controller. 

A requisição retornará uma resposta contendo muitos campos. Neste caso, armazenamos essa resposta em *order_result* e retornamos esse resultado. Utilizaremos esses dados para incrementar nossa lógica de negócio e realizar os tratativos necessários.

**Uma observação importante** é que receber a response não é indicativo de ausência de erros. Como a response pode possuir campos demais para uma boa visualização pelo terminal, considere copiar a response para um arquivo separado e usar o Ctrl+F para pesquisar campos específicos. Procure pelos campos de ‘error’ para saber se tudo ocorreu bem - muitas vezes, haverá uma mensagem bem descritiva sobre a natureza do erro.