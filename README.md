# Bem-Vindo à Wiki da {struct}

Este é um espaço no Gitbook com o objetivo de concentrar todo o conhecimento possível da Struct em um só lugar.

## Conteúdo

Neste espaço deve-se concentrar todos os conhecimentos de gestão e execução de projetos assim como gestão da Struct em si. Por favor, contribua toda vez que verificar que algo está faltando. Caso tenha dúvidas de como trabalhar aqui, acesse a documentação do [Gitbook](https://docs.gitbook.com/content-editing).

### Como Contribuir

#### Git e GitHub

Para realizar modificações nas páginas do Gitbook, é necessário ter um conhecimento básico em alguns conceitos de git, como: add, commit, pull, clone, push e branch. Caso não possua domínio sobre esses conceitos ou deseje revisar algum, a Struct possui um material apresentando uma explicação sucinta [dos principais comandos](https://drive.google.com/file/d/1tH0LaDnD14pHnqq4cymkAjvYX5wkVrCs/view?usp=sharing). Caso queira obter informações mais detalhadas, pode-se consultar o livro *[Pro Git](https://git-scm.com/book/en/v2)* gratuitamente.

##### Observações importantes:

- Use, preferencialmente, a branch de desenvolvimento da sua diretoria para fazer mudanças;
- **Jamais** faça mudanças diretamente na master \(boatos de que quem o fez não está mais na Struct para contar a história\);
- Antes de abrir um pull request, verifique o funcionamento da branch no ambiente de deploy;
- Quando abrir um pull request, peça para alguém da diretoria de Adm-Fin revisar.

#### Repositório do Gitbook

Para começar a trabalhar no Gitbook, clone o [repositório no GitHub](https://github.com/StructEC/gitbook/), acesse a branch da sua diretoria e começe a fazer as modificações nela. É recomendado avisar os outros membros da sua diretoria, para que não haja duas pessoas trabalhando na mesma branch ao mesmo tempo.

#### Padrões Utilizados no Gitbook

##### Arquivos Markdown

Markdown é uma ferramenta que converte texto para HTML, sendo possível marcar títulos, listas, tabelas, etc., de forma muito mais limpa e legível do que o HTML padrão. Caso deseje aprender como escrever em arquivos markdown, seria interessante dar uma olhada em sua [sintaxe básica](guia-markdown.md).

##### Funcionamento

O Gitbook exibe os arquivos markdown de um repositório do Github na forma de páginas web, além de possibilitar a organização destas páginas em várias seções e subpáginas, sendo a disposição das mesmas definida no arquivo *SUMMARY.md*. Vale ressaltar que nem sempre o markdown que funciona no GitHub irá funcionar no Gitbook, portanto é **essencial** checar o funcionamento da página no ambiente de deploy para corrigir possíveis falhas.

###### Sumário

No arquivo *SUMMARY.md* é feita toda a organização das páginas do Gitbook da seguinte forma:  
* Na primeira linha colocamos `# Table of contents` para indicar ao Gitbook que o arquivo se trata do menu lateral que será usado para organizar as páginas.  
* No menu lateral, para criar novas seções sem uma página principal bastar colocar `* Nome da Seção`.
* Para adicionar uma página ao Gitbook basta colocar `* [Nome da página](caminho/arquivo.md)`.
* Caso seja desejado a criação de subpáginas ou subseções, utiliza-se dessa mesma sintaxe, porém identada em relação a seção superior.

##### Estrutura de Pastas

Para agrupar páginas relacionadas a um determinado tópico, é criado uma nova pasta, incluindo nela arquivos cujo conteúdo deriva deste tópico. Por exemplo, o arquivo *instalacao-ruby-on-rails.md* vai estar no diretório *execucao/ruby-on-rails*. Em particular, os arquivos de imagem, devem ser armazenados na pasta *imagens*.

##### Padrões de Nomenclatura

O nome de cada arquivo e pasta se refere ao principal tópico abordado nele, sendo, para arquivos markdown e diretórios, escrito com letra minúscula e para separação de palavras utiliza-se '-'. Em cada diretório, o arquivo da página principal será denotado por `README`.

Arquivos de imagem não possuem restrições quanto ao formato das letras e para separação de palavras geralmente é utilizado '_'.
