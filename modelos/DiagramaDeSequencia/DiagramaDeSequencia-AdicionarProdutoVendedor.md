@startuml
autonumber
actor Vendedor
participant AppVendedor as "Painel do Vendedor"
participant ProdutoService as "Microsserviço de Produtos"
participant ModeracaoService as "Microsserviço de Moderação"
participant NotificacaoService as "Microsserviço de Notificações"
actor Administrador
participant PainelAdmin as "Painel do Administrador"

Vendedor -> AppVendedor: Acessar 'Adicionar Produto'
Vendedor -> AppVendedor: Preencher dados do produto
AppVendedor -> ProdutoService: criarProduto(dados)
ProdutoService --> AppVendedor: produtoCriado(id)
AppVendedor --> Vendedor: exibir "Produto em moderação"

ProdutoService -> ModeracaoService: enviarParaAnalise(produtoId)
ModeracaoService -> NotificacaoService: notificarModerador(produtoId)
NotificacaoService --> PainelAdmin: exibir notificação

Administrador -> PainelAdmin: Acessar painel de moderação
Administrador -> PainelAdmin: Aprovar/Rejeitar produto
PainelAdmin -> ModeracaoService: enviarDecisao(decisao, produtoId)
ModeracaoService -> ProdutoService: atualizarStatus(produtoId, novoStatus)

alt Produto Aprovado
    ProdutoService -> NotificacaoService: notificarVendedor("Aprovado")
else Produto Rejeitado
    ProdutoService -> NotificacaoService: notificarVendedor("Rejeitado")
end
@enduml