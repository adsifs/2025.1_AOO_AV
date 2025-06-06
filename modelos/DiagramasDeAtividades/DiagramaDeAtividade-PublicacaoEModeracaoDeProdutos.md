@startuml
' Título do Diagrama
title Diagrama de Atividade - Publicação e Moderação de Produto

' Definição das "raias" (swimlanes)
|Vendedor|
:start;
:"Acessa o painel e clica em 'Adicionar Novo Produto'";
:"Preenche o formulário com os detalhes do produto\n(nome, preço, estoque, imagens, etc.)";
:"Submete o formulário";

|Sistema Nexus|
:"Recebe os dados do produto";
:"Realiza validação automática inicial";
note right

- Campos obrigatórios preenchidos?
- Preço é um valor positivo?
- Imagens estão no formato correto?
  end note

if (Validação automática OK?) then (sim)
:"Cria o produto no banco de dados com status 'Pendente de Moderação'";
:"Adiciona o novo produto na fila de moderação do Administrador";

    |Administrador|
    :"Acessa o painel de moderação";
    :"Seleciona um produto pendente para revisar";
    :"Analisa os detalhes do produto";
    note right: Verifica se o produto não viola as políticas da plataforma.

    if (Produto está de acordo com as políticas?) then (Aprovar)
        :"Clica em 'Aprovar Produto'";

        |Sistema Nexus|
        :"Altera o status do produto para 'Ativo'";
        note right: Produto agora está visível e disponível para compra.
        :"Envia notificação de aprovação para o Vendedor";

    else (Rejeitar)
        :"Clica em 'Rejeitar Produto'";
        :"Escreve o motivo da rejeição";

        |Sistema Nexus|
        :"Altera o status do produto para 'Rejeitado'";
        :"Envia notificação de rejeição para o Vendedor, incluindo o motivo";
    endif

else (não)
:"Exibe mensagem de erro para o Vendedor, indicando os problemas";
|Vendedor|
-> "Preenche o formulário com os detalhes do produto\n(nome, preço, estoque, imagens, etc.)";
detach
endif

:stop;

@enduml
