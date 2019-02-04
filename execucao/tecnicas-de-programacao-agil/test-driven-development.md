# Test-Driven Development (TDD)

Test-Driven Development (Desenvolvimento Orientado a Testes) é uma metodologia de desenvolvimento em que os testes são escritos antes do código em si e são utilizados para direcionar a criação de código. Essa metodologia é a melhor forma de, no longo prazo, usar seu tempo eficientemente e ao mesmo tempo evitar que problemas apareçam no seu código.

### Ciclo TDD

No Test-driven development, o ciclo de desenvolvimento que o programador deve adotar é constituído pelos seguintes passos:

1. Crie um teste automatizado para uma funcionalidade de um módulo. Certifique-se de que esse teste falha porque o código necessário ainda não foi escrito _(e não porque o teste foi escrito de forma errada)_.
2. Escreva a **menor quantidade** de código possível para que o novo teste passe, mas sem quebrar qualquer teste escrito anteriormente.
3. Caso necessário, refatore o código de forma que todos os testes ainda passem. Também é possível modificar os testes para melhor refletir a funcionalidade desejada. Ao final, retorne para o passo 1.

Esse ciclo de desenvolvimento garante que os requisitos de uma funcionalidade (expressos na forma de testes) dirijam o desenvolvimento de código e que apenas o código estritamente necessário para a funcionalidade será escrito.

### Características de um bom teste

Procure sempre criar testes automatizados que possuam as seguintes qualidades:

* Rapidez: Testes automatizados devem ser rápidos para permitir que eles sejam executados várias vezes.
* Independência: Testes automatizados não devem ser influenciados por testes anteriores, de forma que qualquer teste ou conjunto de testes possa ser executado a qualquer hora.
* Repetibilidade: Testes automatizados devem ter o mesmo resultado se executados várias vezes seguidas, não dependendo, assim, de aleatoriedade.
* Auto-verificação: Testes automatizados devem informar automaticamente ao programador se o teste falhou ou foi bem sucedido.
* Paridade: Os testes automatizados devem sempre ser desenvolvidos em par com o código da aplicação, de forma que os dois não estejam disconexos.

### Vantagens do TDD

* Garante a corretude do seu código perante o cliente e outros programadores.
* Diminui exponencialmente o tempo gasto com debugging.
* Permite que uma refatoração seja feita sem quebrar alguma parte do código.
* Diminui o esforço gasto com testes manuais.

### Desvantagens do TDD

* Requer paciência do programador, mesmo para tarefas supostamente simples.
* No curto prazo, consome mais tempo que o desenvolvimento normal.
* Requer o domínio de uma _DSL (Linguagem de domínio específico)_ para a escrita dos testes.

### TDD em Ruby on Rails

O Test-driven development em Ruby on Rails é feito por meio da gem _RSpec_, permitindo a criação de testes de unidade e de módulo para models, controllers, views e helper modules.

###### Disciplinas do curso que abordam esse conteúdo:
* Métodos de programação (3º Semestre)
* Técnicas de programação I (4º Semestre)
* Engenharia de software (6º Semestre)
