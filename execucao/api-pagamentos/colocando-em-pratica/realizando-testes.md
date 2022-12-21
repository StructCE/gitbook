Seguindo a lógica disposta nos exemplo anteriores, podemos fazer testes de chamadas utilizando o console do rails. Para isso, execute no diretório do Rails API:

```bash
rails c
```

Para realizar a chamada, utilize uma instância do objeto relacionado (no caso dos exemplos, definimos a chamada dos métodos proxy por meio da model Pedido) e chame o método adequado. Para não precisarmos criar uma instância de Pedido a cada uso do console, considere definir essas instâncias previamente na seeds.rb. Dessa forma, podemos testar instâncias com parâmetros variados e ter mais clareza na condução dos testes. Para realizar testes de pagamentos de forma efetiva, refira-se à [seção de Simuladores dos Guias Pagar.me](https://docs.pagar.me/docs/o-que-é-um-simulador).

Dada uma instância do Pedido, podemos fazer:

```ruby
p = Pedido.find(1)
p.create_pedido_proxy('boleto', nil)
```
