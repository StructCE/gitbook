# Uso do Factory Bot

Com o factory bot instalado, podemos criar nossa primeira fábrica para usarmos nos nossos testes. Para isso, dentro da pasta **spec** vamos criar uma subpasta chamada de **factories** na qual ficará todas nossas fábricas para usarmos. Por ora, só precisamos de uma que seria a fábrica para criarmos os estudantes, então, dentro da pasta **factories** criaremos um arquivo chamado **student.rb**.

Dentro desse arquivo, temos a sintaxe básica para começarmos a criar uma factory:

```ruby
FactoryBot.define do 
    
end
```

Dentro desse escopo, podemos começar a criar nossos estudantes para testar, para isso, fazemos o seguinte:

```ruby
FactoryBot.define do 
    factory :student do 
        name { 'Aluno' }
        age { 20 }
    end
end
```

O que estamos fazendo nesse código é, basicamente, criando uma factory do tipo student, refere-se à model, e estamos preenchendo os campos desse student, no caso demos o nome de Aluno e uma idade de 20. Agora, podemos usar com o Rspec para testar.

```ruby
RSpec.describe Student, type: :model do
  context 'check name' do 
    it 'when the name is ok' do
      estudante = build(:student)
      expect(estudante).to be_valid
    end
  end
end
```

Nesse caso, o que estamos fazendo é adicionando a factory que criamos a variável estudante. Seria algo como fazer:

`estudante = Student.new(name:'Aluno', age: 20)`

No entanto, estamos fazendo de uma maneira mais sofisticada usando aquela sintaxe. Vale ressaltar que, no lugar do build, também podemos usar o create, a diferença é que o build não salva no banco de dados, já o create salva, porém, há casos nos quais não se pode usar o build.

Tudo bem, entendemos como fazer no caso de um usuário com todos os parâmetros certos, mas e nos outros exemplos, como faríamos?

Bem simples:

```ruby
RSpec.describe Student, type: :model do
  context 'check name' do 
    it 'when the name is ok' do
      estudante = build(:student)
      expect(estudante).to be_valid
    end

    it 'when the student does not have a name' do
      estudante = build(:student, name:nil)
      expect(estudante).to_not be_valid
    end

    it 'when the name has less than 3 characters' do
      estudante = build(:student, name:"oi")
      expect(estudante).to_not be_valid
    end
  end
end
```

O que fizemos de diferente foi mudar o parâmetros que queríamos testar dentro do build, no exemplo do estudante não ter um nome, passamos dentro no nosso build o **name:nil** e funcionou da mesma maneira.

Caso rodemos o rspec, notaremos que em nenhum dos exemplos teremos erro.

Percebe-se que com o factory bot é um código bem mais conciso e menos poluído.