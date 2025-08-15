@startuml
autonumber
actor Cliente
participant AppCliente as "Aplicativo/Site"
participant PedidoService as "Microsserviço de Pedidos"
participant NotificacaoService as "Microsserviço de Notificações"

Cliente -> AppCliente: Acessar 'Meus Pedidos'
AppCliente -> PedidoService: consultarPedidos(clienteId)
PedidoService --> AppCliente: listaPedidos
AppCliente -> Cliente: exibir pedidos

alt Cliente abre disputa
    Cliente -> AppCliente: abrirDisputa(pedidoId)
    AppCliente -> PedidoService: registrarDisputa(pedidoId)
    PedidoService --> AppCliente: confirmaçãoDisputa
    AppCliente --> Cliente: exibir status da disputa
    PedidoService -> NotificacaoService: notificarVendedor('disputa_aberta')
else Cliente solicita devolução
    Cliente -> AppCliente: solicitarDevolucao(pedidoId)
    AppCliente -> PedidoService: registrarDevolucao(pedidoId)
    PedidoService --> AppCliente: confirmaçãoDevolucao
    AppCliente --> Cliente: exibir status de devolução
    PedidoService -> NotificacaoService: notificarVendedor('devolucao_solicitada')
end
@enduml