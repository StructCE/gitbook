# Bem-Vindo à Wiki da {struct}

Este é um space no gitbook com o objetivo de concentrar todo o conhecimento possível da struct em um só lugar.

## Conteúdo

Neste _space_ deve-se concentrar todos os conhecimentos de gestão e execução de projetos assim como gestão da struct em si. Por favor contribua toda vez que vir algo faltando. Caso tenha dúvidas de como trabalhar aqui, acesse a documentação do [Gitbook](https://docs.gitbook.com/content-editing).

### Como Contribuir

#### Git e GitHub

Para realizar modificações nas páginas do gitbook, é necessário ter um conhecimento básico em alguns conceitos de git, como: add, commit, pull, clone, push e branch. Caso não possua domínio sobre esses conceitos ou deseje revisar algum, a struct possui um material apresentando uma explicação sucinta [dos principais comandos](https://drive.google.com/file/d/1tH0LaDnD14pHnqq4cymkAjvYX5wkVrCs/view?usp=sharing), caso queira obter informações mais detalhadas, pode-se consultar o livro *[Pro Git](https://git-scm.com/book/en/v2)* gratuitamente.

##### Observações importantes:

- Use/crie uma branch adequada para fazer mudanças. Não utilize caracteres especiais como '&' no nome da branch, pois isso quebra o gitbook;
- **Jamais** faça mudanças diretamente na master \(boatos de que quem o fez não está mais na Struct para contar a história\);
- Antes de abrir um pull request, verifique o funcionamento da branch no ambiente de deploy;
- Quando abrir um pull request, peça para alguém revisar.

#### Repositório do Gitbook

Para começar a trabalhar no gitbook, clone o [Repositório no GitHub](https://github.com/StructEC/gitbook/), crie uma nova branch e começe a fazer as modificações nela.

#### Padrões Utilizados no Gitbook

##### Arquivos Markdown

Markdown é uma ferramenta que converte texto para HTML, sendo possível marcar títulos, listas, tabelas, etc., de forma muito mais limpa e legível do que o HTML padrão. Caso deseje aprender como escrever em arquivos markdown, seria interessante dar uma olhada em sua [sintaxe básica](https://www.markdownguide.org/basic-syntax/).

##### Funcionamento

O gitbook exibe os arquivos markdown de um repositório do github na forma de páginas web, além de possibilitar a organização destas páginas em várias seções e subpáginas, sendo a disposição das mesmas definida no arquivo *SUMMARY.md*. Vale ressaltar que nem sempre o markdown que funciona no GitHub irá funcionar no Gitbook, portanto é **essencial** checar o funcionamento da página no ambiente de deploy para corrigir possíveis falhas.

###### Sumário

No arquivo *SUMMARY.md* é feita toda a organização das páginas do gitbook da seguinte forma:  
Na primeira linha colocamos `# Table of contents` para indicar ao gitbook que o arquivo se trata do menu lateral que será usado para organizar as páginas.  
No menu lateral, para criar novas seções sem uma página principal bastar colocar `* Nome da Seção`. Para adicionar uma página ao gitbook basta colocar `* [Título da página](caminho/para/arquivo.md)`. Caso seja desejado a criação de subpáginas ou subseções, utiliza-se dessa mesma sintaxe, porém identada em relação a seção superior.

##### Estrutura de Pastas

Para agrupar páginas relacionadas a um determinado tópico, é criado uma nova pasta, incluindo nela arquivos cujo conteúdo deriva deste tópico. Por exemplo, o arquivo *instalacao-ruby-on-rails.md* vai estar no diretório *execucao/ruby-on-rails*. Em particular, os arquivos de imagem, devem ser armazenados na pasta *imagens*.

##### Padrões de Nomenclatura

O nome de cada arquivo e pasta se refere ao principal tópico abordado nele, sendo, para arquivos markdown e diretórios, escrito com letra minúscula e para separação de palavras utiliza-se "-". Em cada diretório, o arquivo da página principal será denotado por "*README*".  
Arquivos de imagem não possuem restrições quanto ao formato das letras e para separação de palavras geralmente é utilizado "_".

##### Headers

Os headers devem ser organizados de forma decrescente e nunca deve-se pular nível, portanto o header H1 \(# Header\) deve ser reservado apenas para o título da página.

#### Algumas Dicas Sobre Markdown

- Link sem deixar a URL exposta: `[Título do Link](URL)`;
- Imagem: `![Título](caminho-para/imagem.jpg)`;
- Link para outro arquivo markdown: `[Título desejado](caminho-para/página.md)`;
- Link para outro tópico do próprio markdown: `[Título a ser mostrado](#titulo-do-header)`, sendo o título do header em letras minúsculas, separação de palavras com hífen e sempre utilizar apenas um único `#`, independente do tamanho do header;
- Pequeno trecho de código: `` `<p>use a crase<\p>` ``;
- Trecho extenso de código:  
````
```
<li> use </li
<li> três </li>
<li> crases </li>
```
````

- Tabelas: use pelo menos 3 hífens (-) para criar o título de cada coluna e use '|' para separar as colunas:

```
Syntax      | Description
----------- | ----------- 
Header      | Title       
Paragraph   | Text     
```