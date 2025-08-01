@startuml
' Título do Diagrama
title Diagrama de Atividade - Mediação de Disputas pelo Administrador

' Definição das "raias" (swimlanes)
|Sistema Nexus|
:start;
:"Recebe caso de disputa escalado pelo Vendedor";
:"Altera o status da disputa para 'Aguardando Mediação'";
:"Adiciona o caso na fila de revisão do Administrador";

|Administrador|
:"Acessa o painel de mediação e seleciona um caso";
:"Analisa todas as informações do caso";
note right

- Reclamação inicial do Cliente
- Defesa e evidências do Vendedor
- Histórico de mensagens
- Detalhes do pedido
- Reputação de ambas as partes
  end note

if (Decide em favor do Cliente?) then (sim)
:"Registra a decisão final e um parecer no sistema";
:"Clica em 'Resolver em favor do Cliente'";

    |Sistema Nexus|
    fork
        :"1. Envia notificação ao Cliente com a decisão e \ninstruções para devolução (se aplicável)";
    fork again
        :"2. Envia notificação ao Vendedor informando a decisão";
    fork again
        :"3. Inicia o processo de estorno para o Cliente";
        |Sistema de Pagamento|
        :"Processa o estorno do valor";
        |Sistema Nexus|
    end fork
    :"Altera o status da disputa para 'Resolvida pela Mediação'";

else (não, em favor do Vendedor)
:"Registra a decisão final e um parecer no sistema";
:"Clica em 'Resolver em favor do Vendedor'";

    |Sistema Nexus|
    fork
        :"1. Envia notificação ao Cliente com a decisão final";
    fork again
        :"2. Envia notificação ao Vendedor com a decisão final";
    fork again
        :"3. Libera o pagamento que estava retido para o Vendedor";
    end fork
    :"Altera o status da disputa para 'Rejeitada pela Mediação'";

endif

:stop;

@enduml
