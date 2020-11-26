# Dicas ninjas

## Otho

- Se não aparecer nada na pagina, pode ser um dos seguintes problemas:

  - Erro no HTML

  - Erro no arquivo `application.js`, pois um erro em alguma parte do código acarreta no mal funcionamento de todo o JS. Portanto, certifique-se sempre de que tudo la dentro esta certo!

- Se não aparecer alguma coisa na views algo que envolve código Ruby, verifique as tags `<%` ou `<%=`

- Se há um uso de framework, certifique-se se ela exige inicialização do js.(Ler documentação do framework).

- Ao se fazer merge de branches, verifique se não houve junção de linhas fantasmas ou tags sem par nos arquivos de código resultante(Muito cuidado nos códigos influenciados, principalmente .HTML !!!). A chance de ocorrer problemas nessa etapa é alta.

- Cuidado com o turbolinks!!! Ele às vezes acarreta no mal funcionamento de frameworks e códigos do JS.

- Se houver erro bizarro, verifique o turbolinks. Algumas vezes o turbolinks "crasha" os recursos da página, desde JS até o rails(pode acreditar!).

- Erros do tipo uninitialize constant AlgumaCoisa::OutraCoisa (Esse erro é uma m*$#$%): Geralmente o erro ou está no controller ou nos arquivos da pasta models. Verifique se as variáveis usadas foram inicializadas no controller; e se os nomes nos arquivos da pasta `app/models/`, checando as letras maiúsculas nas classes e aspas ou o símbolo ":"
