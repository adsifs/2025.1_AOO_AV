stateDiagram-v2
%% Diagrama de Estados para o Objeto Pagamento no formato Mermaid

    state fork_state <<fork>>
    [*] --> fork_state
    fork_state --> AguardandoPagamento : boletoGerado
    fork_state --> EmProcessamento : cartaoEnviado ou pixIniciado

    AguardandoPagamento : (Boleto) Aguardando pagamento do cliente.
    AguardandoPagamento --> Aprovado : compensacaoBancariaConfirmada / notificarSistema()
    AguardandoPagamento --> Cancelado : boletoExpirou [evento de tempo]

    EmProcessamento : (Cartão/Pix) Aguardando resposta do gateway.
    EmProcessamento --> Aprovado : gatewayConfirmaPagamento / notificarSistema()
    EmProcessamento --> Recusado : gatewayRecusaPagamento / notificarSistema()

    Aprovado : Transação bem-sucedida.
    note right of Aprovado
        Este evento dispara a atualização
        do status do Pedido para "Pago".
    end note
    Aprovado --> Estornado : estornoSolicitadoPeloSistema
    Aprovado --> [*] : transacaoConcluida

    Recusado : Pagamento negado pela instituição financeira.
    Recusado --> [*]

    Cancelado : Pagamento não concluído no prazo.
    Cancelado --> [*]

    Estornado : Valor devolvido ao cliente.
    Estornado --> [*]
