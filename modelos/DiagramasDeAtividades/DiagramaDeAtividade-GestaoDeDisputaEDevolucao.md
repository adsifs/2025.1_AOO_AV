@startuml
' Título do Diagrama
title Diagrama de Atividade - Gestão de Disputa e Devolução

' Definição das "raias" (swimlanes)
|Cliente|
:start;
:"Acessa 'Meus Pedidos' e abre uma disputa/devolução";
:"Preenche o motivo e anexa evidências (fotos, etc.)";

|Sistema Nexus|
:"Cria um registro de 'Disputa'";
:"Altera o status do pedido para 'Em Disputa'";
note right: O pagamento ao vendedor pode ser retido neste ponto.
:"Notifica o Vendedor sobre a nova disputa";

|Vendedor|
:"Acessa o painel e analisa a disputa";

if (Aceita a solicitação do cliente?) then (sim)
' Caminho da Resolução Amigável
:"Aprova a devolução no sistema";

    |Sistema Nexus|
    :"Gera etiqueta de logística reversa";
    :"Envia a etiqueta para o Cliente";

    |Cliente|
    :"Embala o produto e o posta nos Correios/transportadora";

    |Vendedor|
    :"Recebe o produto devolvido";
    :"Confirma o recebimento e a condição do item";

    |Sistema Nexus|
    :"Recebe a confirmação do vendedor";
    :"Inicia o processo de estorno do pagamento";
    note right: Aciona o Gateway de Pagamento para realizar o estorno.
    :"Envia e-mail de confirmação do estorno para o Cliente";
    :"Fecha a disputa como 'Resolvida'";

else (não)
' Caminho da Mediação
:"Contesta a solicitação no sistema";
:"Apresenta sua defesa e evidências";

    |Sistema Nexus|
    :"Altera o status da disputa para 'Aguardando Mediação'";
    :"Coloca a disputa na fila de revisão do Administrador";

    |Administrador|
    :"Analisa o caso completo (argumentos do cliente e do vendedor)";

    if (Decide em favor do Cliente?) then (sim)
        :"Registra a decisão final";
        ' O fluxo se junta ao caminho da resolução amigável, forçado pelo admin
        |Sistema Nexus|
        -> "Gera etiqueta de logística reversa";
        detach

    else (não, em favor do Vendedor)
        :"Registra a decisão final";
        |Sistema Nexus|
        :"Envia notificação da decisão para ambas as partes";
        :"Fecha a disputa como 'Rejeitada pela Mediação'";
        :"Libera o pagamento para o Vendedor";
    endif

endif

:stop;

@enduml
