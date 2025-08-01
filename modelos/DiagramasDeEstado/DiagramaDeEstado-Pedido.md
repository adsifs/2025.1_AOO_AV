stateDiagram-v2
%% Diagrama de Estados para o Objeto Pedido no formato Mermaid

    [*] --> Pendente : pedidoCriado

    Pendente : O pedido foi criado. Aguarda pagamento.
    Pendente --> Pago : pagamentoConfirmado / notificarVendedor()
    Pendente --> Cancelado : pagamentoRecusado
    Pendente --> Cancelado : pedidoCanceladoPeloUsuario

    Pago : Pagamento aprovado. Vendedor prepara o envio.
    Pago --> Enviado : produtoDespachado / notificarClienteComRastreio()
    Pago --> Cancelado : cancelamentoPorFraude [pelo Admin]

    Enviado : Produto em trânsito para o cliente.
    Enviado --> Entregue : entregaConfirmada

    Entregue : Cliente recebeu o produto.
    note right of Entregue
        Inicia o prazo de segurança
        (ex: 14 dias) para o repasse
        ao vendedor.
    end note
    Entregue --> EmDisputa : disputaAberta / reterPagamento()
    Entregue --> Finalizado : prazoDeDisputaExpirou

    EmDisputa : Cliente abriu uma reclamação.
    EmDisputa --> Finalizado : disputaResolvida

    Finalizado : Pedido concluído com sucesso.
    Cancelado : Pedido não foi concluído.

    Cancelado --> [*]
    Finalizado --> [*]
