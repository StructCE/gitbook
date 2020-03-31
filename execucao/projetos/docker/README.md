# Docker

O Docker é um ambiente de virtualização que utiliza recursos isolados no sistema operacional, mas compartilha bibliotecas do *kernel* do sistema operacional entre o host e o container. O host é a máquina que está rodando o sistema operacional e o container é nosso ambiente virtualizado. Podemos ter múltiplos containers, onde cada container pode ter ferramentas específicas e os containers podem se comunicarem entre si. A maior vantagem do Docker é que podemos empacotar uma aplicação inteira \(no caso, o nosso app do Rails ou o nosso banco de dados para o app\).

## Recursos criados com o Docker

* Imagens: As imagens são templates do container que queremos criar, no caso da Struct essas imagens ficam armazenadas no Docker Hub.

* Containers: Os containers são instâncias da execução dos pacotes que compõe um programa, admitindo suas particularidades ao funcionarem. Em outras palavras, um container é a imagem em execução ou o que a imagem se torna em memória em tempo de execução.

* Network: O network nos permite gerenciar a rede dos containers e como será feita a comunicação entre containers. Se 2 containers estão na mesma rede, eles se comunicam diretamente; se não, eles precisam de outra forma para se comunicarem.

* Ports: Os ports são portas que estarão visíveis para acesso a algum recurso de um container a partir de qualquer lugar da internet. Isso ocorre desde que a porta esteja liberada para acesso ao servidor, ou para acesso a partir do host ou de qualquer container, mesmo se esse container não estiver na mesma rede que o container original. Um exemplo do uso de ports é o *Ruby on Rails*, onde normalmente usamos a porta 3000 e liberamos essa porta para que outros containers que não estejam na mesma rede possam acessá-lo. Outra porta comumente utilizada é a porta 80, que liberamos para fornecer acesso http a algum container.

* Volume: O volume funciona como um local permanente armazenado pelo Docker no host para que, mesmo se o container for destruído, os dados não sejam perdidos.
