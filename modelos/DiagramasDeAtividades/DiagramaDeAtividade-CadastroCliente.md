@startuml
' Título do Diagrama
title Diagrama de Atividade - Cadastro de Novo Cliente

' Definição das "raias" (swimlanes)
|Visitante|
:start;
:"Clica no botão 'Cadastrar'";

|Sistema Nexus|
:"Exibe a página com o formulário de cadastro";

|Visitante|
:"Preenche os dados solicitados\n(Nome, E-mail, Senha, CPF)";
:"Clica em 'Criar Conta'";

|Sistema Nexus|
:"Recebe os dados do formulário";
:"Realiza validações nos dados";
note left

- Todos os campos obrigatórios foram preenchidos?
- O e-mail tem um formato válido?
- O CPF tem um formato válido?
- O e-mail ou CPF já existem no sistema?
  end note

if (Dados são válidos e únicos?) then (sim)
:"Cria a conta do usuário no banco de dados com status 'Pendente'";
note right: A senha é armazenada usando um hash seguro,\nNUNCA como texto plano.
:"Gera um token de verificação de e-mail";
:"Envia o e-mail de verificação para o endereço fornecido";
:"Exibe uma página de sucesso com a mensagem:\n'Cadastro realizado! Verifique seu e-mail para ativar a conta.'";

    |Visitante|
    :"Abre seu cliente de e-mail";
    note right: Esta ação ocorre fora da plataforma Nexus.
    :"Clica no link de verificação recebido no e-mail";

    |Sistema Nexus|
    :"Recebe a requisição do link de verificação";
    :"Valida o token";
    :"Altera o status do usuário para 'Ativo'";
    :"Realiza o login automático do usuário";
    :"Redireciona para a página principal ou painel do cliente";

else (não)
:"Exibe novamente o formulário de cadastro";
:"Mostra mensagens de erro específicas\n(Ex: 'E-mail já cadastrado', 'CPF inválido')";
-> "Preenche os dados solicitados\n(Nome, E-mail, Senha, CPF)";
detach
endif

:stop;
@enduml
