@startuml
autonumber
actor Vendedor
participant AppVendedor as "Painel do Vendedor"
participant ProdutoService as "Microsserviço de Produtos"
participant NotificacaoService as "Microsserviço de Notificações"

Vendedor -> AppVendedor: Acessar 'Gerenciar Produtos'
AppVendedor -> ProdutoService: listarProdutos(vendedorId)
ProdutoService --> AppVendedor: produtosListados
AppVendedor --> Vendedor: exibir lista de produtos

alt Criar Produto
    Vendedor -> AppVendedor: preencher dados do produto
    AppVendedor -> ProdutoService: criarProduto(dados)
    ProdutoService --> AppVendedor: produtoCriado(id)
    AppVendedor --> Vendedor: exibir sucesso
    ProdutoService -> NotificacaoService: notificarVendedor("Produto criado com sucesso")
else Editar Produto
    Vendedor -> AppVendedor: editarProduto(id, dados)
    AppVendedor -> ProdutoService: atualizarProduto(id, dados)
    ProdutoService --> AppVendedor: produtoAtualizado
    AppVendedor --> Vendedor: exibir sucesso
    ProdutoService -> NotificacaoService: notificarVendedor("Produto atualizado com sucesso")
end

alt Excluir Produto
    Vendedor -> AppVendedor: excluirProduto(id)
    AppVendedor -> ProdutoService: removerProduto(id)
    ProdutoService --> AppVendedor: produtoRemovido
    AppVendedor --> Vendedor: exibir sucesso
    ProdutoService -> NotificacaoService: notificarVendedor("Produto excluído com sucesso")
end
@enduml