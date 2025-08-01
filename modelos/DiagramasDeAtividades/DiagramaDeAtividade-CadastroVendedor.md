@startuml
' Título do Diagrama
title Diagrama de Atividade - Cadastro e Aprovação de Vendedor

' Definição das "raias" (swimlanes)
|Cliente/Aspirante a Vendedor|
:start;
:"Acessa seu perfil e clica em 'Quero Vender'";

|Sistema Nexus|
:"Exibe formulário de cadastro de vendedor";

|Cliente/Aspirante a Vendedor|
:"Preenche dados adicionais\n(Loja, CNPJ/CPF, Dados Bancários, etc.)";
:"Envia o formulário";

|Sistema Nexus|
:"Recebe e valida os dados do formulário";
note right: Validação automática de formato,\n preenchimento de campos obrigatórios, etc.

if (Validação automática OK?) then (sim)
    :"Salva o cadastro com status 'Pendente de Aprovação'";
    :"Coloca a solicitação na fila de revisão do Administrador";
    
    |Administrador|
    :"Acessa o painel e seleciona uma solicitação pendente";
    :"Analisa as informações e documentos do vendedor";
    
    if (Aprova o cadastro?) then (sim)
        :"Muda o status do usuário para 'Aprovado'";
        
        |Sistema Nexus|
        :"Altera o papel do usuário para 'Vendedor'";
        :"Libera o acesso ao Painel do Vendedor";
        :"Envia e-mail de boas-vindas ao novo vendedor";
        
    else (não)
        :"Informa o motivo da rejeição";
        |Sistema Nexus|
        :"Registra o motivo e altera o status para 'Rejeitado'";
        :"Envia e-mail de notificação de rejeição ao usuário";
    endif

else (não)
    :"Exibe mensagem de erro indicando os campos inválidos";
    -> "Preenche dados adicionais\n(Loja, CNPJ/CPF, Dados Bancários, etc.)";
    detach
endif

|Cliente/Aspirante a Vendedor|
:stop;

@enduml