@startuml
autonumber
actor Cliente
participant AppCliente as "Aplicativo/Site"
participant PedidoService as "Microsserviço de Pedidos"
participant EstoqueService as "Microsserviço de Estoque"
participant PagamentoGateway as "Gateway de Pagamento"
participant NotificacaoService as "Microsserviço de Notificações"

Cliente -> AppCliente: Iniciar Finalização de Compra
AppCliente -> PedidoService: criarPedido(carrinho)
PedidoService -> EstoqueService: reservarEstoque(itens)
EstoqueService --> PedidoService: confirmação de reserva
PedidoService -> PagamentoGateway: solicitarPagamento(pedido)
PagamentoGateway --> PedidoService: respostaPagamento(status)

alt Pagamento Aprovado
    PedidoService -> PedidoService: atualizarStatus(status='PAGO')
    PedidoService --> AppCliente: compraConfirmada()
    AppCliente --> Cliente: exibir sucesso
    PedidoService -> NotificacaoService: enviarNotificacao('pedido_recebido')
else Pagamento Recusado
    PedidoService -> EstoqueService: liberarEstoque(itens)
    PedidoService --> AppCliente: falha no pagamento
    AppCliente --> Cliente: exibir erro
end
@enduml