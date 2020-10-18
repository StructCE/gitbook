# Gamificação
O sistema de gamificação da Struct é um sistema com base em pontos com objetivo de motivar os membros da empresa e recompensar os que mais trabalham. A gamificação é composta por um sistema de pontos, organizando os membros em patentes de acordo com sua pontuação e uma premiação para os membros que mais se destacarem em uma temporada (6 meses).

Como o sistema ainda se encontra nas fases iniciais de implementação, as informações vistas abaixo não devem ser vistas como definitivas, com modificações podendo ser realizadas com o amadurecimento do sistema.

## Sistema de pontos
A gamificação é centrada em um sistema de pontos que são dados ou retirados aos membros com base nas tarefas realizadas por cada um. Esses pontos são contabilizados mensalmente, com uma média mensal dos 6 meses sendo realizada no fim da temporada.
A pontuação final de um membro é calculada usando a seguinte fórmula:
> pontuação final = horas do mês + pontos adicionais

As **horas do mês** são a quantidade de horas trabalhadas pelo membro, dentre as 6 horas mínimas exigidas, com a relação *1 hora = 1 ponto*. Haverá também uma pontuação extra por horas trabalhadas acima do mínimo semanal.
Os **pontos adicionais** são a contabilização de todos os pontos ganhos ou perdidos de acordo com os critérios definidos na tabela abaixo:

Pontuação | Descrição | Frequência
------------ | ------------- | -------------
+3 pontos | Caso o membro seja gerente de projeto | Mensal
+3 pontos | Caso o membro seja diretor | Mensal
+3 pontos | Caso o membro seja instrutor de trainee | Mensal
+3 pontos | Para membros de destaque indicados por um diretor ou gerente de projeto | Mensal
+3 pontos | Participação em 1 projeto | Mensal
+5 pontos | Participação em 2 projetos | Mensal
+1 ponto | Para cada participação adicional em projeto acima de 2 | Mensal
-3 pontos | Faltas não justificadas em reuniões | Por falta
-3 pontos | Mensagens origatórias não respondidas (ex: *daily*) | Por mensagem
-3 pontos | Atrasos em projetos ou tarefas da diretoria | Por atraso
-0,5 pontos | Hora não trabalhada abaixo da média de horas semanais (6 horas) | Por hora

### Patentes
A pontuação obtida pelos membros é utilizada para posicioná-los em uma posição em um esquema de patentes, sendo essas:

Ranking | Patente | Pontuação Mensal
------------ | ------------- | -------------
1 | Marechal do Cosmos | Top 1
2 | Mestre das armas | Top 2
3 | Major Sideral | Top 3
4 | Engenheiro de ignição | 50
5 | Chefe de máquinas | 34
6 | Especialista de colisões | 24
7 | Técnico do motor de dobra | 16
8 | Analista de campo gravitacional | 10
9 | Operador do reator nuclear | 6
10 | Assistente de escudo refletor | 0

As primeiras três patentes só podem ser ocupadas por um membro cada e tem como condição de entrada a obtenção de no mínimo 60 pontos. Caso apenas um membro consiga atingir a pontuação mínima do top 3, ele ocupará automaticamente a primeira posição.

## Premiação
A cada 6 meses ocorrerá a finaliazação da temporada de pontos, sendo criada uma média mensal dos pontos obtidos pelos membros e posicinando-os na escala final de patentes.
Os membros que se posicionarem entre as posições 4 e 6 do ranking terão prêmios mais simples enquanto os no top 3 obterão os melhores prêmios da temporada.

## Aplicativo
Está em desenvolvimento interno na Struct um aplicativo para acompanhamento do sistema pelos membros da empresa, com visualização de sua posição no ranking de patentes e projeção de qual será sua próxima patente de acordo com o seu desempenho atual. O objetivo é que o aplicativo também permita a contabilização automática das horas do clockfy e contabilização de pontos para os diretores e gerentes de projeto, inclusive com a seleção dos membros de destaques por estes, para contabilização dos pontos extras.
