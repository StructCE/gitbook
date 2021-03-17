# Guia Markdown
As páginas do Gitbook são compatíveis com a sintaxe Markdown para sua estilização, incluindo padrões para definição de títulos, listas e estilização de texto. Além disso, o Gitbook também é compatível com o Markdown extendindo do Github e com sintaxe exclusiva da plataforma

## Títulos
O Markdown é compatível com até 6 níveis de títulos, utilizando cerquilhas `#` antes da frase. Uma cerquilha é o título de maior destaque e 6 o de menos.
Os headers devem ser organizados de forma decrescente e nunca deve-se pular nível. Portanto o header H1 (`#` Header) deve ser reservado apenas para o título da página.
### Exemplo de uso
```
# Título 1
## Título 2
### Título 3
#### Título 4
##### Título 5
###### Título 6
```

## Linha horizontal
Você pode adicionar uma linha horizontal na página usando `***` ou `---`. Se houver um texto na linha imediatamente acima, usando a sintaxe `---`, esse texto irá virar um header do tipo 2.
***

## Estilização de texto
O Markdown permite que seu texto fique em **negrito**, _itálico_ e, com a extensão do Github, ~riscado~.

Estilo | Comando | Alternativa
------- | ----------- | -------
_Itálico_ | `_Underline_` | `*Asterisco*`
**Negrito** | `__Underline duplo__` | `**Asterisco duplo**`
***Itáilico e negrito*** | `***Asterisco triplo***` | `**_Asterisco e underline_**`

## Listas
É possível a criação de listas ordenadas e desordenadas. Com a extensão do Github, também é possível a criação de checklists.

* Para listas desordenadas voce pode utilizar um asterisco simples `*` antes da linha
	* Você também pode usar `tab` antes do asterisco para ir para um próximo nível da lista
- Você também pode usar `-` no lugar do asterisco


1. Para listas ordenadas use o número seguido de um ponto `1.`
	* É possível meslcar listas ordenadas com desordenadas


- [ ] Para uma checklist use `- [ ]` para definir um item em aberto
- [x] Para um item terminado, use `- [x]`

## Tabelas
Para criação de uma tabela em Markdown, separe as colunas usando barra vertical `|` e o header da coluna das outras linha usando hífens `-`. Note que essa é uma sintaxe da extensão do Github e pode não funcionar em outros sites não compatíveis.
### Exemplo de uso
```
Coluna 1 | Coluna 2
-------- | --------
Item 1.1 | Item 1.2
Item 2.1 | Item 2.2
```
## Citações
> Você pode adicionar citações nos seus textos utilizando `>` antes da linha.

## Código em linha
É possível adicionar pequenos trechos de código em uma linha, no estilo `int x = 10`. Essa ferramenta também é útil para `enfatizar` trechos do texto. Para fazer isso `` `use essa sintaxe` ``.

## Bloco de código
É possível, também, adicionar um bloco de código utilizando ` ``` ` para abrir e fechar o bloco. Usando os padrões do Github, você definir a linguagem a ser utilizada no bloco, para fins de estilização, escrevendo o nome da linguagem após o comando de abertura do bloco.
### Exemplo de uso
````
```ruby
x = 10
@Products = Product.all.order('name ASC')
```
`````

## Links
É possível inserir [links](http://google.com) para sites externos ou mesmo para outras páginas do [Gitbook](README.md), usando o caminho para o arquivo. Para fazer isso use a estrutura `[links](http://google.com)`. 

Para link para outro [tópico](#titulos) do próprio Markdown use `[Título a ser mostrado](#titulo-do-header)`, sendo que o título do header deve estar em letras minúsculas, com separação de palavras com hífen, com 'c' ao invés de 'ç', e com apenas um único `#`, independente do tamanho do header;

## Imagens
Inserir uma imagem é similar à inserção de links, usando a sintaxe `![Imagem](https://i.imgur.com/0Y6Qh0Z.png)`. Para imagens dentro do repositório do Gitbook, use o caminho para a imagem.

## Dicas
{% hint style="info" %} 
É possível a adição de blocos de dicas no meio de seu texto.
{% endhint %}

{% hint style="success" %} 
A seguinte sintaxe é usada:
```
{% hint style="info" %} 
Hello world
{% endhint %}
```
{% endhint %}

{% hint style="warning" %} 
Os estilos de dicas disponíveis são `info`, `success`, `warning` e `danger`.
{% endhint %}

{% hint style="danger" %}
Essa sintaxe é exclusiva do Gitbook e pode não funcionar em outras ferramentas, como o Github.
{% endhint %}
