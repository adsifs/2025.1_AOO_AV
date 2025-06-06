stateDiagram-v2
%% Diagrama de Estados para o Objeto Produto no formato Mermaid

    [*] --> EmRascunho : vendedorCriaProduto

    EmRascunho : Vendedor está criando o anúncio.
    EmRascunho --> PendenteDeModeração : vendedorEnviaParaRevisão

    PendenteDeModeração : Aguardando aprovação de um Administrador.
    PendenteDeModeração --> Ativo : adminAprova / notificarVendedor()
    PendenteDeModeração --> Rejeitado : adminRejeita / notificarComMotivo()

    Rejeitado : Anúncio rejeitado pela moderação.
    Rejeitado --> EmRascunho : vendedorEditaAnuncio

    Ativo : Visível e disponível para compra.
    Ativo --> Pausado : vendedorPausaVendas
    Ativo --> Esgotado : estoqueChegaAZero [evento do sistema]
    Ativo --> Arquivado : vendedorRemoveAnuncio

    Pausado : Indisponível para venda por ação do vendedor.
    note right of Pausado
        O produto pode continuar visível,
        mas sem o botão de comprar.
    end note
    Pausado --> Ativo : vendedorReativaVendas
    Pausado --> Arquivado : vendedorRemoveAnuncio

    Esgotado : Sem estoque disponível.
    Esgotado --> Ativo : vendedorAdicionaEstoque
    Esgotado --> Arquivado : vendedorRemoveAnuncio

    Arquivado : Anúncio removido das listagens ativas.
    Arquivado --> [*]
