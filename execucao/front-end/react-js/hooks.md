# Hooks

O react possibilita a criação de componentes. Mas e quando queremos que o html renderizado pelo componente seja atualizado junto com alguma variável do javascript? Nos componentes funcionais (sem ser feitos com classes), usamos os [hooks](https://reactjs.org/docs/hooks-reference.html).

### Um problema:

Queremos fazer um contador, onde sempre que um botão é clicado, um número que aparece na tela aumenta. Porém, podemos ver que isso não funciona:

```jsx
import { Container } from "./styles";

const Counter = () => {
	var count = 1;

	const handleCounterIncrement = () => {
		counter = counter + 1;
	};

	return (
		<Container>
			<p>Counter: {counter}</p>
			<button onClick={handleCounterIncrement}>Increment</button>
		</Container>
	);
};
export default Counter;
```

## useState

Função que recebe um estado inicial e retorna uma variável e um setter.

Serve para declarar variáveis com as quais se deseja sincronizar o conteúdo da página. Por exemplo:

```jsx
import { Container } from "./styles";
import { useEffect, useState } from "react";

const Counter = () => {
	const [count, setCount] = useState(0);

	const handleCounterIncrement = () => {
		setCount(counter + 1);
	};

	return (
		<Container>
			<p>Count value = {count}</p>
			<button onClick={handleCounterIncrement}>Increment</button>
		</Container>
	);
};
export default Counter;
```

## useEffect

Função que recebe um callback (arrow function) e um array de dependências. Quando o componente for rerenderizado, se alguma das variáveis do array de dependências tiver mudado, o callback é executado.
Se o array de dependência não for especificado, o useEffect vai ser executado em toda mudança de estado, possivelmente causando um loop infinito. Nesses casos, geralmente o que se deseja utilizar é um array vazio.

Serve principalmente para sincronizar um efeito com alguma mudança de variável. Por [exemplo](https://codesandbox.io/s/hooks-demo-0otg5h):

```jsx
import { Container } from "./styles";
import { useEffect, useState } from "react";

const Counter = () => {
	const [count, setCount] = useState(0);

	// acrescentando um efeito que é disparado na primeira renderização, e depois sempre que count muda:
	useEffect(() => {
		console.log(count);
		if (count === 1) {
			alert("count === 1 is true");
			// some logic
		}
	}, [count]);

	return (
		<Container>
			<p>Count value = {count}</p>
			<button onClick={() => setCount(count + 1)}>Increment</button>
		</Container>
	);
};
export default Counter;
```

## useContext

Serve para criar um contexto. Considere uma aplicação web inteira que é baseada num usuário logado. Usando o que conhecemos até agora, teríamos que guardar o usuário na raíz da aplicação e passar pra todos os filhos que precisam (praticamente todos) o usuário e funções (como a de login) por _props_.
Mas e se pudéssemos fazer um estado global, acessível sem ser apenas pelas _props_? É exatamente isso que é o contexto.

Exemplos:
https://codesandbox.io/s/usecontext-demo-qtugvt?file=/src/contexts/UserContext.js
https://www.youtube.com/watch?v=Zz4icNdPzTM