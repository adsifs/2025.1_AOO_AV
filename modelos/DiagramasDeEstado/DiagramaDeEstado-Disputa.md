stateDiagram-v2
    %% Diagrama de Estados para o Objeto Disputa no formato Mermaid

    [*] --> Aberta : disputaCriadaPeloCliente / notificarVendedor()

    Aberta : Aguardando a primeira ação do Vendedor.
    Aberta --> EmNegociacao : vendedorResponde / notificarCliente()
    Aberta --> Resolvida : vendedorAceitaDevolucao / iniciarDevolucao()
    Aberta --> AguardandoMediação : vendedorEscalaParaAdmin

    EmNegociacao : Cliente e Vendedor estão em diálogo.
    EmNegociacao --> EmNegociacao : clienteResponde ou vendedorResponde
    note right of EmNegociacao
        Esta seta que aponta para o próprio estado
        representa o "bate-papo" entre as partes.
    end note
    EmNegociacao --> Resolvida : acordoAlcancado / processarAcordo()
    EmNegociacao --> AguardandoMediação : disputaEscalada [por qualquer parte]
    EmNegociacao --> Fechada : clienteCancelaDisputa

    AguardandoMediação : Caso escalado. Aguardando decisão do Administrador.
    AguardandoMediação --> Resolvida : adminDecidePeloCliente / forcarResolucao()
    AguardandoMediação --> Fechada : adminDecidePeloVendedor / liberarPagamento()

    Resolvida : Disputa encerrada a favor do Cliente.
    Resolvida --> [*]

    Fechada : Disputa encerrada (sem ganho para o Cliente).
    Fechada --> [*]