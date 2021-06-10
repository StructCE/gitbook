# Assinatura digital de documentos
A Struct tem a necessidade constante de assinar documentos, desde contratos com clientes até atas de eleição. Em um contexto de trabalho remoto, e até mesmo quando não há opção de ter a presença de todos os envolvidos na assinatura, nós nos voltamos à assinatura digital de documentos. Na Struct usamos a ferramenta [Clicksign](https://app.clicksign.com/) para esse fim.
## Usando o Clicksign
Primeiro tenha em mão o login e senha da Struct para acessar o portal da ferramenta, se você não tiver, entre em contato com seu diretor ou presidente para obtê-los.
### Inserindo um documento para a assinatura

![Tela do site Clicksign](../../imagens/clicksign-main.png)

Após seu login, você verá a organização de pastas da ferramenta. Navegue até a pasta que corresponde ao tipo de documento que você vai adicionar (sinta-se livre para criar novas pastas para fins de organização). Na pasta desejada, clique no botão *Adicionar documento*, localizado na barra lateral esquerda, e selecione o documento PDF ou Word no seu computador que você deseja colocar para assinatura.

![Tela de signatários](../../imagens/clicksign-signatarios.png)

Com o documento carregado, você irá para a página de selecionar os signatários, onde você terá duas escolhas:
#### *Signatário novo*

![Tela de novo signatario](../../imagens/clicksign-novo-signatario.png)

Aqui você terá que digitar o e-mail do signatário e no campo *Autenticação Obrigatória* selecionar *Enviar token por E-mail*. Não é necessário colocar nada no campo de *Autenticações adicionais*.
Você tem a opção de preencher os campos de CPF, nome e data de nascimento também, mas não é obrigatório, visto que será perguntado ao signatário caso esteja em branco. Caso deseje, marque o checkbox para adicionar o contato na agenda.
Avance e selecione na lista como o signatário deve assinar. Caso esteja em dúvida, deixe como *Assinar*.

![Tela de tipo de assinatura](../../imagens/clicksign-tipo-assinatura.png)

#### *Signatário da agenda*
Alguns contatos normalmente já se encontram salvos em nossa agenda do Clicksign, como os diretores e presidente. Se o contato desejado já estiver na lista, é só selecioná-lo e selecionar como ele deverá assinar. Novamente, caso esteja em dúvida, deixe como *Assinar*.

{% hint style="warning" %}
Evite deixar nossa agenda do Clicksign muito cheia e bagunçada. Insira como contato novo apenas pessoas recorrentes, como nossos membros.
{% endhint %}
#### Seleção de data limite

![Tela de data limite](../../imagens/clicksign-data.png)

Após selecionar todos os signatários, você irá ver a página se seleção de data limite. As configurações padrões normalmente são as utilizadas pela empresa, mas sinta-se livre para estender ou diminuir a data limite, como achar necessário.
Apenas na seção *Finalização do Documento* que faça questão de deixar para finalizar automaticamente após a última assinatura, por fins de praticidade. 
#### Mensagem

![Tela de inserção de mensagem](../../imagens/clicksign-mensagem.png)

Por fim, coloque a mensagem que será enviada por e-mail para a assinatura. Ao apertar botão logo abaixo da área da mensagem, você terá a opção de selecionar a mensagem padrão, a recomendada a ser utilizada pela empresa.
Com isso, clique em *Enviar* e os e-mails para coleta das assinaturas serão enviados para os signatários.
### Como realizar a assinatura
Para assinar um documento no Clicksign, verifique na caixa de entrada do e-mail cadastrado como pertencente ao signatário. No e-mail enviado pela ferramenta, terá um link para a assinatura do documento, em que será possível tanto verificar o documento quanto assiná-lo. Para assinar, um novo e-mail será enviado com um token de 6 caracteres para ser inserido. E fim, fácil e rápido para fazer uma assinatura.
### Acompanhando documentos em processo
No link *Em Processo* na barra lateral do site é possível acompanhar todos os documentos ainda não finalizados. Ao selecionar um dos documentos, temos algumas opções interessantes:
#### Adicionar novos signatários
Na aba *Assinaturas* você pode adicionar signatários que faltaram durante a adição do documento, seguindo os mesmos passos de [antes](#signatario-novo)
#### Cancelar documento
Na mesma aba *Assinaturas* há o botão de *Cancelar*, se por algum motivo você deseja cancelar o documento em processo. Note que, se cancelado, todas as assinaturas obtidas serão anuladas.
#### Mudar prazo de assinatura
É comum clientes mais enrolados demorarem muito para assinar um documento, em especial termos de conclusão. Nessa situação pode ocorrer do documento está chegando em sua data limite com assinaturas ainda não coletadas.
Para contornar isso, na aba *Configurações* você pode modificar a data limite para permitir ao cliente um tempo maior de assinar, e impedindo que o documento seja finalizado com assinaturas faltando.
### Obtendo documentos finalizados
Documentos finalizados são enviados para o e-mail de admin da Struct e para os e-mail de todos os signatários. Além disso, na barra lateral do site, é possível ir para a seção *Finalizados* e visualizar os últimos documentos finalizados. Lembrando que, a não ser que você tenha mudado as configurações padrões, os documentos serão automaticamente finalizados assim que a última assinatura for realizada. Por fim, selecione o documento desejado e faça um download de sua cópia assinada.

{% hint style="warning" %} 
O Clicksign não é um drive para armazenamento de documentos, visto que ele não garante que documentos antigo não sejam excluídos. Dessa forma, sempre faça o download dos documentos que você inseriu e foram finalizados e os adicione no drive da empresa.
{% endhint %}

### Pagamento da ferramenta
Nosso plano do Clicksign nos permite a assinatura de até 5 documentos gratuitos por mês, com cada documento adicional custando R$ 5,00.
No caso de superarmos nosso limite mensal, o pagamento deverá ser feito pelo diretor administrativo-financeiro, usando preferencialmente boleto bancário. Para acessar a página de pagamento vá até a opção de *Configurações* na barra lateral e na aba de *Cobrança*.
Note que, o não pagamento em dia das dívidas do Clicksign bloqueia nosso acesso ao site, até que seja pago, e gera uma pequena multa.
### Validade de documentos impressos do Clicksign
Ás vezes, temos a necessidade de imprimir algum documento do Clicksign, para envio ao cartório, por exemplo. No entanto, por si só, o documento assinado digitalmente não tem validade se for impresso então para contornar isso, usamos o [validador do Clicksign](https://validador.clicksign.com/).

![Tela do validador](../../imagens/clicksign-validador.png)

Nesse site, clique na opção de gerar senha a partir de um PDF e selecione o PDF do documento que você deseja imprimir.  Feito isso, você terá acesso a uma senha e QR Code de acesso para validação do documento. Imprima essa página junto do documento para que ele seja legalmente aceito de forma impressa.