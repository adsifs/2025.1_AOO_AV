@startuml
title Processamento de Devolução - Nexus Marketplace

package "Fluxo de Solicitação e Processamento de Devolução" {

    ' --- Etapa do Usuário ---
    [Interface de Usuário] --> [Serviço de Solicitação de Devolução] : Usuário solicita devolução
    [Serviço de Solicitação de Devolução] --> [Banco de Dados de Devoluções] : Registra solicitação

    ' --- Etapa de Processamento Automático ---
    [Serviço de Solicitação de Devolução] --> [Serviço de Processamento de Devolução] : Envia solicitação para processamento

    [Serviço de Processamento de Devolução] --> [Serviço de Verificação de Prazo] : Checa se ainda está dentro do prazo permitido
    [Serviço de Processamento de Devolução] --> [Serviço de Validação de Condições] : Verifica status do pedido, pagamento e possíveis disputas

    [Serviço de Verificação de Prazo] --> [Serviço de Tomada de Decisão de Devolução]
    [Serviço de Validação de Condições] --> [Serviço de Tomada de Decisão de Devolução]

    [Serviço de Tomada de Decisão de Devolução] --> [Banco de Dados de Devoluções] : Atualiza status (Aprovada/Rejeitada)
    [Serviço de Tomada de Decisão de Devolução] --> [Serviço de Notificação] : Informa vendedor e comprador sobre resultado

}

package "Serviços Externos" {
[Serviço de Notificação]
}

database "Banco de Dados de Devoluções" as DBDevolucoes

@enduml
