@startuml
' Título do Diagrama
title Diagrama de Atividade - Repasse Financeiro ao Vendedor (Payout)

' Definição das "raias" (swimlanes)
|Sistema Nexus|
:start;
note left: Processo iniciado por uma tarefa agendada\n(Ex: executa toda noite à 1h da manhã).

:"Busca por todas as vendas com status de pagamento 'Pendente ao Vendedor'";

if (Existem vendas a serem pagas?) then (sim)
-> A; ' Conector para a próxima etapa
else (não)
:stop;
endif

' Label A para continuar o fluxo
label A
:"Para cada Vendedor com saldo a receber...";
note right
O sistema agrupa todas as vendas elegíveis
de um mesmo vendedor para fazer um único repasse.
end note

:"Calcula o valor total a ser repassado";
note right: (Soma das Vendas Elegíveis) - (Comissão do Nexus)

:"Envia uma requisição de transferência para o Gateway de Pagamento";

|Sistema de Pagamento|
:"Recebe a requisição e processa a transferência bancária";

if (A transferência foi bem-sucedida?) then (sim)
:"Envia confirmação de sucesso para o Sistema Nexus";

    |Sistema Nexus|
    :"Recebe a confirmação";
    :"Atualiza o status das vendas pagas para 'Repassado ao Vendedor'";
    :"Envia uma notificação de pagamento para o Vendedor com o extrato";

else (não)
:"Envia notificação de erro para o Sistema Nexus";
note right: Motivos comuns: dados bancários incorretos, instabilidade no banco, etc.

    |Sistema Nexus|
    :"Recebe a notificação de erro";
    :"Mantém o status das vendas como 'Pendente ao Vendedor'";
    :"Cria um alerta no painel do Administrador para revisão manual";

    |Administrador|
    :"Recebe e analisa o alerta de falha no pagamento";
    note right: O Administrador deverá contatar o vendedor para corrigir os dados.

endif

-> "Busca por todas as vendas com status de pagamento 'Pendente ao Vendedor'";

@enduml
