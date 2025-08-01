stateDiagram-v2
    %% Diagrama de Estados para o Objeto Vendedor no formato Mermaid

    [*] --> PendenteDeAprovação : solicitacaoEnviada

    PendenteDeAprovação : Aguardando análise e aprovação de um Administrador.
    PendenteDeAprovação --> Ativo : adminAprova / notificarVendedor()
    PendenteDeAprovação --> Rejeitado : adminRejeita / notificarComMotivo()

    Ativo : Vendedor aprovado. Pode vender na plataforma.
    Ativo --> Suspenso : adminSuspendePorViolacao / pausarAnuncios()
    Ativo --> Inativo : vendedorEncerraConta

    Suspenso : Conta bloqueada por um Administrador.
    note right of Suspenso
        Sanção imposta pela
        plataforma por violação
        de políticas.
    end note
    Suspenso --> Ativo : adminReverteSuspensao / reativarAnuncios()
    Suspenso --> Inativo : vendedorEncerraConta

    Inativo : Vendedor encerrou sua loja voluntariamente.
    Rejeitado : Solicitação para ser vendedor foi negada.

    Rejeitado --> [*]
    Inativo --> [*]