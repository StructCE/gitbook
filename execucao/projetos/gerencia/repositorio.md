# Repositório

A criação do repositório para o projeto deve ser feita no grupo da Struct do GitLab. O nome do repositório geralmente segue o padrão `projeto_nome` ou `projeto_codinome` \(como gerente de projeto, sinta-se livre para criar um codinome épico para o projeto :grinning:\). Configure o repositório como privado e **não** inicialize ele com um README, pois o Rails já gera esse arquivo para você. Após criar o repositório, faça o upload dos arquivos gerados pelo projeto de Rails para o repositório.

## Criação de branches padrão

Um projeto bem estruturado contém um conjunto de branches padrões e um fluxo bem definido que novas features ou mudanças em features existentes devem percorrer para serem aprovadas definitivamente e chegarem aos clientes da aplicação. O gerente de projetos é o responsável por criar e configurar as branches padrões no repositório do projeto no GitHub. Também cabe ao gerente de projetos garantir que o desenvolvimento siga o fluxo definido pelas branches padrões, evitando a utilização de atalhos e os problemas gerados pela quebra do fluxo de desenvolvimento.

Esta seção detalha as branches padrão que todo projeto da Struct deve ter, com uma breve descrição do seu propósito geral e fluxo de desenvolvimento.

#### Develop

A **develop** é a branch de desenvolvimento padrão. Ela deve ser marcada como *default* e *protected* nas configurações de branch do projeto. Todas as features desenvolvidas devem ser adicionadas primeiramente à *develop* por meio de um *Pull request*.

#### Main

A **main** é a branch da versão oficial do software para os desenvolvedores. Se possível, ela deve ser marcada como *protected* nas configurações de branch do projeto. De tempos em tempos, as features desenvolvidas na branch *develop* são levadas a branch *main* por meio de um *Pull request*, permitindo ao time de desenvolvedores revisar com mais afinco e atenção as features desenvolvidas \(tipicamente, no final da *sprint*\). Além disso, a *main* pode ser utilizada para receber diretamente correções de *bugs* ou problemas críticos, sem a necessidade dessas correções urgentes se misturarem com as features novas da *Develop*, encurtando o caminho de desenvolvimento até o cliente.

#### Production

A **production** é a branch da versão oficial do software para os clientes. Se possível, também deve ser marcada como *protected* nas configurações de branch do projeto. De tempos em tempos, as features testadas e revisadas presentes na branch *main* são levadas à branch *production* por meio de um *Pull request* para que essas mudanças cheguem efetivamente aos clientes do projeto e possam ser utilizadas ou visualizadas pelos usuários do produto. Tenha muito cuidado ao colocar mudanças nessa branch, pois qualquer falha ou erro terá **consequências reais** para o cliente e para os usuários da aplicação.
