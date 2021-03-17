# Ruby vs Ruby on Rails
O Ruby é uma linguagem de programação interpretada que contém uma ferramenta de gerenciamento chamada de RubyGems. Essa ferramenta é responsável por instalar e gerenciar as gems, que são bibliotecas de código aberto que expandem a funcionalidade do Ruby.
O Ruby on Rails (RoR) é exatamente isso, uma gem para Ruby, que permite e facilita o desenvolvimentos de sites orientados a banco de dados. A instalação do Ruby, portanto, é necessária para utilizar o Rails.
Note também que, tanto o Ruby quanto suas gems (incluindo o Rails) têm versões específicas e diferentes. Ou seja, os projetos aqui da Struct terão duas versões importantes a serem observadas, a do Ruby e a do Rails.
# Instalação do Ruby
Há três maneiras de instalar o Ruby em sua máquina, cabe a você decidir qual a melhor para a sua utilização.
## Instalação única
Aqui será instalado apenas uma versão do Ruby na sua máquina. Esse método de instalação é o menos recomendado, já que você ficará limitado a utilizar apenas uma versão do Ruby.
Na Struct, por exemplo, nós acabamos, por vezes, utilizando diferentes versões do Ruby e do Rails em diferentes projetos, e trocar entres essas versões sem utilizar um gerenciador de versões pode se tornar uma dor de cabeça, ou seja, dê preferência pela instalação de algum gerenciador de versões.
### Windows
Para instalar o Ruby no windows [acesse esse link](https://rubyinstaller.org/downloads/) e baixe o instalador da versão requerida. Siga os passos do instalador e o Ruby estará instalado em seu PC.
Durante a instalação, certifique-se de marcar a opção de instalar o MSYS2. No final da instalação, também irá aparecer um checkbox para rodar o  *ridk install*, marque-o também. Após isso, irá ser aberto um terminal do CMD para finalizar a instalação, nessa etapa, você pode simplesmente apertar enter para fazer a instalação padrão.
Para verificar a instalação, abra o CMD ou o PowerShell e digite `ruby -v`, o retorno deverá ser a versão instalada do Ruby.
### Linux ou Windows Subsystem for Linux
Comece verificando se o Ruby já se encontra instalado em seu computador, utilizando o comando `ruby -v` no terminal. Caso retorne a versão do Ruby, ele já se encontra instalado no seu PC.
Se você utiliza Ubuntu, Debian, Mint ou outros derivados de Debian Linux como sua distribuição Linux, execute os seguintes comandos no terminal para instalar o Ruby:
```bash
sudo apt update
sudo apt-get install ruby-full
```
Note que os comandos acima apenas funcionam se você utiliza Ubuntu, Debian, Mint ou outros derivados de Debian Linux como sua distribuição Linux. Para outras distribuições, procure o Ruby no gerenciador de pacotes da distribuição.
Por fim, verifique sua instalação com o comando `ruby -v`.
## Gerenciador de versão
A melhor forma para instalar e utilizar o Ruby é usando um gerenciador de versões. Esses gerenciadores permitem que você instale uma variedade de versões do Ruby em uma mesma máquina e alterne à vontade entre elas. Há, no Linux, dois gerenciadores de versões mais utilizados, o RBenv e o RVM. O RBenv oferece uma instalação mais leve que o RVM, não contendo todas as funcionalidades do outro (normalmente pouco utilizadas).
Para utilização aqui na Struct, não há diferenças perceptíveis entre a utilização das duas.
Note que no Windows não há um bom gerenciador de versão em pleno suporte. Para essa funcionalidade, é recomendado usar o Windows Subsystem for Linux.
### RBenv
Há duas formas diferentes de instalar o RBenv em seu computador, clonando o repositório do git ou usando o curl.
#### Clonando o repositório do git
Primeiro, iremos clonar e instalar o RBenv. No seu terminal, digite os seguintes comandos:
```bash
cd
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
exec $SHELL
```
Em seguida, instalaremos o ruby-build, que permitirá a instalação das versões do Ruby juntamente com o RBenv:
```bash
git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc
exec $SHELL
```
Agora use o comando `rbenv -v` para verificar a instalação do RBenv.
#### Usando Curl
Outra opção para instalar o RBenv é usando o curl. Comece instalando-o, caso não esteja ainda instalado:
```bash
sudo apt update
sudo apt install curl
```
No terminal, digite o seguinte comando para obter o script de instalação da ferramenta. Note que com esse comando, tanto o RBenv quanto o ruby-build, para instalação das versões do Ruby, já são instalados.
```bash
curl -fsSL https://github.com/rbenv/rbenv-installer/raw/master/bin/rbenv-installer | bash
```
O output deverá ser o seguinte:
```bash
output
Running doctor script to verify installation...
Checking for `rbenv' in PATH: not found
  You seem to have rbenv installed in `/home/<username>/.rbenv/bin', but that
  directory is not present in PATH. Please add it to PATH by configuring
  your `~/.bashrc', `~/.zshrc', or `~/.config/fish/config.fish'.
```
Agora deveremos colocar o RBenv no PATH:
```bash
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
source ~/.bashrc
```
Agora use o comando `rbenv -v` para verificar a instalação do RBenv.
#### Instalando o ruby com o RBenv
Com qualquer umas das maneiras acima, a instalação de qualquer versão do Ruby usando o RBenv é a mesma.
Usando o comando `rbenv install -l` você pode verificar todas as versões disponíveis para instalação. Aqui iremos instalar a versão 2.7.2, que neste momento é a versão estável mais recente disponível, mas fique livre para instalar a versão utilizada no projeto atual que você está trabalhando ou qualquer outra a sua escolha. Digite o seguinte comando no terminal:
```bash
rbenv install 2.7.2
```
Para definir a versão instalada como a padrão do seu sistema, use o seguinte comando:
```bash
rbenv global 2.7.2
```
Execute agora o comando `ruby -v` para verificar a instalação.
Para definir uma outra versão do Ruby para ser usada em um projeto execute o seguinte comando:
```bash
rbenv local 2.7.2
```
O comando acima irá criar um arquivo oculto `.ruby-version` no seu diretório atual e todo terminal aberto nele será iniciado com a versão especificada do Ruby. Em outros diretórios, a versão definida com o comando `global` continuará a ser utilizada.
Para usar outra versão do Ruby temporariamente em um terminal, sem salvar essa configuração em algum local, utilize o seguinte comando:
```bash
rbenv shell 2.7.2
```
Se quiser mais detalhes sobre o RBenv, [acesse o repositório oficial do projeto](https://github.com/rbenv/rbenv) e procure algum membro da Struct caso necessite de ajuda em alguma das etapas.
### RVM
Para instalação do RVM, utilizaremos o curl. Comece instalando-o, caso ainda não esteja, juntamente com outras dependências:
```bash
sudo apt update
sudo apt-get install curl libgdbm-dev libncurses5-dev automake libtool bison libffi-dev
```
Utilize o seguinte comando em seguida, para obtenção das chaves GPG, necessárias para a instalação:
```bash
gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
```
Instale o RVM com os seguintes comandos:
```bash
curl -sSL https://get.rvm.io | bash -s stable
source ~/.rvm/scripts/rvm
```
Use o comando `rvm -v` para verificar a instalação.
Feito isso, devemos apenas instalar a versão desejada do Ruby. Você pode usar o comando `rvm list known` para obter uma lista com todas as versões disponíveis. Nesse caso, iremos instalar a 2.7.2, por ser a estável mais recente disponível. Execute o seguinte comando para a instalação:
```bash
rvm install 2.7.2
```
Para definir essa versão como a principal, utilize o seguinte comando:
```bash
rvm use 2.7.2 --default
```
Por fim, execute o comando `ruby -v` para verificar a instalação.
Para utilizar temporariamente outra versão instalada do Ruby, utilize o seguinte comando:
```bash
rvm use 2.7.2
```
Para verificar todas as versões instaladas na sua máquina você pode utilizar o comando `rvm list`
Se quiser mais detalhes sobre o RVM, [acesse o site do projeto](https://rvm.io/) e procure algum membro da Struct caso necessite de ajuda em alguma das etapas.
# Instalação do Rails
Para instalar o Rails abra seu terminal (CMD ou PowerShell no caso do Windows) e execute o seguinte comando:
```bash
gem install rails
```
Para especificar uma versão do Rails a ser instalada use o seguinte comando, mudando a versão passada pela desejada. Note que muitos projetos aqui na Struct ainda utilizam a versão 5 do Rails, mesmo a mais recente sendo a versão 6:
```bash
gem install rails -v 5.2.4.4
```
Caso você esteja utilizando o RBenv, utilize o seguinte comando para deixar o executável do Rails disponível:
```bash
rbenv rehash
```
Por fim, utilize o comando `rails -v` para verificar a instalação.
Para criar um novo projeto em Rails para testar seu funcionamento, utilize os seguinte comandos:
```bash
rails new my_project
cd my_project
rails server
```
Feito isso, acessando o endereço `locahost:3000` em algum navegador deverá te mostrar a página de boas vindas do Rails.
