# Testando models

Para começar a testar as models, vamos criar uma model na nossa aplicação:

`rails g model Student name:string age:integer`

No terminal:

`rails db:migrate`

Dentro da pasta Spec deve ter sido criada uma pasta com o nome de **models** e dentro dessa pasta deve ter um arquivo chamado **student_spec.rb**.

Caso não tenha sido criado automaticamente, será necessário arrumar algumas coisas no pasta Spec. Então, na pasta Spec, criaremos outra pasta com o nome de models, pasta na qual todos os arquivos de teste de model serão colocamos, e, dentro na pasta model, criaremos o arquivo **student_spec.rb**, é importante lembrar que os arquivos de teste sempre terminam com o _spec.rb.

A sintaxe básica no arquivo **student_spec.rb** é:

```ruby
require 'rails_helper'

RSpec.describe Student, type: :model do
  
end
```

A primeira linha é necessária para que peguemos do arquivo **rails_helper** as requisições necessárias para que consigamos rodar nossos testes.

Já na segunda linha, temos o **Rspec.describe Student, type: :model** que nos diz, basicamente, o que estamos testando e de que tipo é a coisa que estamos testando, então, informamos para o Rspec que estamos testando o componente Student e ele é do tipo Model.

Agora que já tá tudo pronto, podemos começar a testar.

```ruby
require 'rails_helper'

RSpec.describe Student, type: :model do
  context 'check name' do 
    it 'when the name is ok' do

    end

    it 'when the name is not ok' do

    end
  end
end
```

O que fizemos agora foi adicionar um contexto(**context**) para o nosso Rspec, nesse contexto eu digo que nosso objetivo é testar o nome do aluno. Dentro desse contexto temos dois **it** que se refere aos casos de teste que estão dentro do contexto, o primeiro é para checar os casos de quando tudo no nome estiver certo, o segundo para checar os casos de quando algo no nome estiver fora do esperado.

Nesse momento, caso usemos o comando **rspec** ou **rspec spec/models/student_spec.rb** no terminal, nos será retornado o seguinte:

`2 examples, 0 failures`

Isso nos informa, basicamente, que temos dois exemplos (os dois it's) e nenhuma falha, até porque, apesar de temos os exemplos de teste, ainda não temos nenhum corpo contendo o que está sendo testado, mas vamos resolver isso agora.

```ruby
require 'rails_helper'

RSpec.describe Student, type: :model do
  context 'check name' do 
    it 'when the name is ok' do
      estudante = Student.new(name:"Aluno", age: 20)
      expect(estudante).to be_valid
    end

    it 'when the name is not ok' do

    end
  end
end
```

Agora, dentro do exemplo que checa se o nome está certo, criamos um aluno por meio do **Student.new** e depois usamos a linha **expect(student).to be_valid**, essa linha basicamente checa se nossa variável **estudante** tem tudo que um nome precisa pra ser válido. Quando rodarmos o comando **rspec** no terminal perceberemos que o resultado é o mesmo do anterior, 2 exemplos e 0 falhas, isso porque na nossa model **student.rb** não tem nenhuma limitação para nome, logo, todo nome que colocarmos vai ser aceito, até mesmo se deixarmos o campo nome vazio, então, é bom consertarmos isso.

Assim sendo, é necessário que criemos algumas validações no nossoa arquivo de model para garantir algumas limitações que o nosso estudante deve ter. Para esse exemplo, eu pensei que todo estudante deve ter um nome, ou seja, o campo nome não pode ser vazio e o estudante tem que ter um nome com, pelo menos, 3 letras.

```ruby
class Student < ApplicationRecord
    validates :name, presence: :true
    validates_length_of :name, minimum: 3
end
```

Então, é exatamente isso que estamos validando na nossa model, a primeira linha diz que o campo nome não pode ser vazio, a segunda diz que o campo nome tem que ter, no mínimo, 3 letras.

Assim sendo, podemos adicionar mais checagens no nosso teste, a primeira que checa se o nome é vazio, caso seja, não pode ser validado e a segunda que checa se o nome tem menos de três letras, caso tenha, também não poderá ser validado.

```ruby
require 'rails_helper'

RSpec.describe Student, type: :model do
  context 'check name' do 
    it 'when the name is ok' do
      estudante = Student.new(name:"Aluno", age: 20)
      expect(estudante).to be_valid
    end

    it 'when the student does not have a name' do
      estudante = Student.new(name:nil, age:20)
      expect(estudante).to_not be_valid
    end

    it 'when the name has less than 3 characters' do
      estudante = Student.new(name:"oi", age:20)
      expect(estudante).to_not be_valid
    end
  end
end
```

Nesse caso, o que fizemos foi basicamente checar nossas outras duas validações, caso o nome esteja vazio ou tenha menos de 3 letras esperamos que o usuário não pode ser criado, caso rodemos esse teste no terminal receberemos de volta o seguinte:

`3 examples, 0 failures`

Então, nossos testes deram certo.

Nesse sentido, seria interessante que fizéssemos validações para a idade do usuário também. Então, na nossa model, podemos fazer algo do tipo:

```ruby
class Student < ApplicationRecord
    validates :name, presence: :true
    validates_length_of :name, minimum: 3

    validates :age, presence: :true
    validates :age, numericality: { greater_than_or_equal_to: 18,  only_integer: true }
end
```

Com as novas validações, eu digo que todo estudante tem que ter uma idade e que essa idade deve ser maior ou igual a 18 e só pode ser do tipo integer.

Caso tenha dúvidas em como fazer validações numéricas, pode acessar a documentação do Rails: [https://guides.rubyonrails.org/active_record_validations.html#numericality](https://guides.rubyonrails.org/active_record_validations.html#numericality).

Agora que nossas validações estão prontas, podemos testar (apesar de que o ideal é fazer os testes primeiro e depois as validações).

```ruby
require 'rails_helper'

RSpec.describe Student, type: :model do
  context 'check name' do 
    it 'when the name is ok' do
      estudante = Student.new(name:"Aluno", age: 20)
      expect(estudante).to be_valid
    end

    it 'when the student does not have a name' do
      estudante = Student.new(name:nil, age:20)
      expect(estudante).to_not be_valid
    end

    it 'when the name has less than 3 characters' do
      estudante = Student.new(name:"oi", age:20)
      expect(estudante).to_not be_valid
    end
  end

  context 'check age' do 
    it 'when the age is ok' do 
      estudante = Student.new(name:'Aluno', age:20)
      expect(estudante).to be_valid
    end

    it 'when the age is not a number' do 
      estudante = Student.new(name:'Aluno', age:'oi')
      expect(estudante).to be_invalid
    end

    it 'when the age is nil' do 
      estudante = Student.new(name:'Aluno', age:nil)
      expect(estudante).to be_invalid
    end

    it 'when the age is less than 18' do 
      estudante = Student.new(name:'Aluno', age:17)
      expect(estudante).to be_invalid
    end
  end
end
```

Agora, fizemos o contexto de checar idade e introduzimos uma nova sintaxe. No lugar de usarmos **expect(estudante).to_no be_valid**, nós usamos o **expect(estudante).to be_invalid**. No final das contas, o resultado será o mesmo e, quando checarmos esses testes, teremos o retorno de 7 exemplos e 0 falhas.