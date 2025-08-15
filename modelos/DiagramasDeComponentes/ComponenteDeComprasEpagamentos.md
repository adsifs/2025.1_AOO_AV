@startuml
title Módulo de Compras e Pagamentos - Nexus Marketplace

package "Módulo de Compras e Pagamentos" {

    [Interface de Usuário] --> [Serviço de Criação de Pedido] : Inicia novo pedido
    [Serviço de Criação de Pedido] --> [Serviço de Finalização de Compra] : Pedido pronto para pagamento
    [Interface de Usuário] --> [Serviço de Acompanhamento de Pedidos] : Consulta status e histórico

    [Serviço de Criação de Pedido] --> [Banco de Dados de Pedidos] : Salva pedido com status "pendente"
    [Serviço de Finalização de Compra] --> [Serviço de Controle de Pagamento] : Processa pagamento
    [Serviço de Finalização de Compra] --> [Banco de Dados de Pedidos] : Atualiza status do pedido

    [Serviço de Controle de Pagamento] --> [Banco de Dados de Pagamentos] : Registra pagamento
    [Serviço de Controle de Pagamento] ..> [Serviço de Notificação] : Notifica cliente sobre pagamento

    [Serviço de Acompanhamento de Pedidos] --> [Banco de Dados de Pedidos] : Lê informações de pedidos

}

package "Serviços Externos" {
    [Serviço de Notificação]
}

database "Banco de Dados de Pedidos" as DBPedidos
database "Banco de Dados de Pagamentos" as DBPagamentos

@enduml
