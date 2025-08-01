@startuml
' Título do Diagrama
title Diagrama de Atividade - Finalização de Compra (Checkout)

' Definição das "raias" (swimlanes) para cada participante do processo
|Cliente|
:start;
:"Clica em 'Finalizar Compra'";

|Sistema Nexus|
if (Cliente está logado?) then (sim)
else (não)
|Cliente|
:"Realiza Login ou Cadastro";
|Sistema Nexus|
endif
:"Exibe resumo do pedido (produtos e endereço)";
:"Calcula o frete para cada vendedor";
:"Apresenta valor total (produtos + frete)";

|Cliente|
if (Aplica cupom de desconto?) then (sim)
|Sistema Nexus|
:"Valida e aplica o cupom";
:"Atualiza o valor total";
endif

|Cliente|
:"Seleciona o método de pagamento";

|Sistema Nexus|
if (Método foi Cartão de Crédito ou Pix?) then (Cartão/Pix)
|Cliente|
:"Informa os dados do pagamento";
|Sistema Nexus|
:"Envia dados para o gateway de pagamento";
|Sistema de Pagamento|
:"Processa a transação";
if (Pagamento Aprovado?) then (sim)
|Sistema Nexus|
:"Recebe confirmação de pagamento";
else (não)
|Sistema Nexus|
:"Informa erro ao cliente";
|Cliente|
-> "Seleciona o método de pagamento";
detach
endif
else (Boleto)
:"Gera o Boleto Bancário";
|Cliente|
:"Visualiza e salva o Boleto";
note right: O processo do pedido prossegue,\nmas aguarda a compensação do boleto.
|Sistema Nexus|
endif

' Fork para ações paralelas do sistema após o sucesso do pagamento
fork
:"1. Deduz itens do estoque dos vendedores";
fork again
:"2. Envia e-mail de confirmação para o Cliente";
fork again
:"3. Cria pedido e notifica os Vendedores";
end fork

:"Exibe página de 'Pedido Confirmado' para o Cliente";

|Cliente|
:stop;
@enduml
