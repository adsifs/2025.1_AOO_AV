# 📃 Diagramas de Atividade




### 1. Cadastro e Autenticação
- Cadastro com nome completo, e-mail e senha.  
- Login via conta Google.  
- Recuperação de senha por e-mail.  
- Senhas armazenadas com hash seguro.  
- Edição e exclusão de conta.  



```puml
@startuml
start

:Usuário acessa a tela de "Cadastro";

if (Usuário escolhe "Recuperar Senha"?) then (Sim)
  :Sistema solicita o e-mail;
  :Usuário informa o e-mail;

  :Sistema verifica se o e-mail está cadastrado;

  if (E-mail cadastrado?) then (Sim)
    :Sistema envia link de recuperação de senha por e-mail;
    :Usuário segue o link para redefinir a senha;
    stop
  else (Não)
    :Sistema exibe mensagem de erro: "E-mail não encontrado";
    stop
  endif

else (Não)

  :Sistema exibe campos:
  - Nome completo
  - E-mail
  - CPF
  - Senha (mínimo 8 caracteres, validação);

  :Usuário preenche os dados e envia o formulário;

  if (Usuário escolhe "Entrar com Google"?) then (Sim)
    :Sistema redireciona para autenticação via OAuth;
    :Usuário autoriza o acesso;
    :Sistema cria ou acessa conta vinculada ao e-mail do Google;
    :Usuário é redirecionado para a tela inicial logado;
    stop
  else (Não)
    :Sistema verifica se o e-mail já está cadastrado;

    if (E-mail já cadastrado?) then (Sim)
      :Sistema exibe mensagem de erro;
      :Impede o cadastro duplicado;
      stop
    else (Não)
      :Sistema verifica se o CPF já está cadastrado;

      if (CPF já cadastrado?) then (Sim)
        :Sistema exibe mensagem de erro;
        :Impede o cadastro duplicado;
        stop
      else (Não)
        :Sistema armazena os dados com criptografia de senha (hash);
        :Sistema cria o registro de usuário;
        :Usuário é redirecionado para a tela inicial logado;
        stop
      endif
    endif
  endif
endif

@enduml
```

### 2. Cadastro de Veículos
- Cadastro de múltiplos veículos por usuário.  
- Campos obrigatórios: marca, modelo, ano, combustível, quilometragem atual, placa.  
- Validação de placa (formatos Mercosul e antigo).  
- Prevenção de placas duplicadas.  
- Indicação de proprietário e motoristas autorizados.  
- Edição e exclusão com controle de permissões.  



```puml
@startuml
start

:Usuário acessa a tela de "Cadastro de Veículo";

:Sistema exibe campos obrigatórios:
- Marca
- Modelo
- Ano
- Combustível
- Quilometragem atual
- Placa;

:Usuário preenche os dados e envia o formulário;

:Sistema valida formato da placa (Mercosul ou antigo);

if (Placa válida?) then (Sim)
  :Sistema verifica duplicidade da placa;

  if (Placa já cadastrada?) then (Sim)
    :Sistema exibe mensagem de erro: "Placa duplicada";
    stop
  else (Não)
    :Sistema cadastra o veículo;
    :Sistema associa o proprietário ao veículo;

    :Usuário escolhe adicionar motoristas autorizados?;

    if (Sim)
      :Usuário seleciona motoristas autorizados;
      :Sistema associa motoristas autorizados ao veículo;
    else (Não)
      note right
      Apenas o proprietário terá acesso inicialmente.
      end note
    endif

    :Sistema confirma cadastro com sucesso;
    stop
  endif

else (Não)
  :Sistema exibe mensagem de erro: "Formato de placa inválido";
  stop
endif

@enduml
```

### 3. Compartilhamento de Veículos
- Compartilhamento via e-mail ou código de convite.  
- Controle de permissões (visualização ou edição).  
- Remoção de acesso a qualquer momento.  
- Notificações de alterações feitas por convidados.  
- Transferência de propriedade do veículo.



```puml
@startuml
start

:Usuário acessa a opção "Compartilhar Veículo";

:Sistema exibe opções:
- Compartilhar via e-mail
- Compartilhar via código de convite;

:Usuário escolhe a forma de compartilhamento;

if (Via e-mail?) then (Sim)
  :Usuário informa o e-mail do convidado;
  :Sistema envia convite com link de acesso;
else (Via código)
  :Sistema gera código de convite;
  :Usuário compartilha o código com o convidado;
endif

:Usuário define permissão:
- Visualização
- Edição;

:Sistema associa permissão ao convidado;

:Convidado aceita o convite;

:Sistema concede o acesso conforme permissão;

:Sistema ativa notificações de alterações ao proprietário;

:Usuário deseja transferir a propriedade?;

if (Sim)
  :Usuário seleciona novo proprietário;
  :Sistema transfere a propriedade;
  :Novo proprietário recebe notificação;
else (Não)
  :Sistema mantém a propriedade original;
endif

:Usuário pode remover acesso de qualquer convidado a qualquer momento;

stop
@enduml
```

### 4. Registro de Manutenções
- Registro de tipo de serviço, data, quilometragem, oficina, valor e observações.  
- Upload de nota fiscal com leitura automática (OCR).  
- Edição e exclusão com rastreamento do autor. 



```puml
 @startuml
start

:Usuário acessa "Registrar Manutenção";

:Sistema exibe campos:
- Tipo de serviço
- Data
- Quilometragem
- Oficina
- Valor
- Observações;

:Usuário preenche dados;

:Usuário faz upload da nota fiscal;

:Sistema processa nota com OCR (leitura automática);

:Sistema armazena os dados e arquivo da nota;

:Usuário pode editar ou excluir registro;

:Sistema rastreia e armazena autor das alterações;

stop
@enduml
```

### 5. Alertas Inteligentes
- Geração de alertas por tempo e quilometragem.  
- Notificações para todos os motoristas vinculados.  
- Sugestões automáticas com base no histórico de manutenções.  
- Cálculo dinâmico de alertas.



```puml
@startuml
start

:Sistema calcula tempo e quilometragem desde última manutenção;

if (Critérios para alerta atingidos?) then (Sim)
  :Sistema gera alerta;

  :Sistema envia notificação a todos os motoristas vinculados;

  :Sistema sugere manutenção com base no histórico;

else (Não)
  :Nenhuma ação necessária;
endif

:Sistema recalcula alertas dinamicamente;

stop
@enduml
```

### 6. Histórico e Relatórios
- Histórico completo por veículo.  
- Filtros por motorista, serviço, oficina e datas.  
- Relatórios promocionais e exportação em PDF.  
- Geração de relatório de entrega de veículo.



```puml
@startuml
start

:Usuário acessa "Histórico e Relatórios";

:Sistema exibe filtros:
- Motorista
- Serviço
- Oficina
- Datas;

:Usuário aplica filtros;

:Sistema exibe histórico completo do veículo;

:Usuário solicita geração de relatório;

if (Tipo de relatório: promocional ou entrega?) then (Entrega)
  :Sistema gera relatório de entrega de veículo em PDF;
else (Promocional)
  :Sistema gera relatório promocional em PDF;
endif

:Usuário faz download do PDF;

stop
@enduml
```

### 7. Atualização de Quilometragem
- Atualização manual da quilometragem.  
- Histórico das atualizações por usuário.  



```puml
@startuml
start

:Usuário acessa "Atualizar Quilometragem";

:Usuário informa nova quilometragem;

:Sistema valida se quilometragem é maior que a anterior;

if (Válida?) then (Sim)
  :Sistema atualiza a quilometragem do veículo;

  :Sistema registra a atualização com identificação do usuário;

  :Sistema armazena no Histórico de Atualizações;

else (Não)
  :Sistema exibe mensagem de erro: "Quilometragem inválida";
endif

stop
@enduml
```

### 8. Módulo de Despesas Gerais
- Registro de despesas como IPVA, seguro, multas, lavagens, etc.  
- Categorização das despesas.  
- Relatórios por mês, categoria e veículo.  



```puml
@startuml
start

:Usuário acessa "Registrar Despesa";

:Sistema exibe campos:
- Tipo de despesa (IPVA, seguro, multa, lavagem etc.)
- Valor
- Data
- Observações;

:Usuário preenche os dados;

:Sistema categoriza a despesa;

:Sistema armazena a despesa no registro do veículo;

:Usuário solicita relatórios;

:Sistema exibe relatórios por:
- Mês
- Categoria
- Veículo;

stop
@enduml
```

### 9. Checklist de Viagem
- Lista sugerida com base no tipo de viagem e revisões.  
- Exportação em PDF.



```puml
@startuml
start

:Usuário acessa "Checklist de Viagem";

:Sistema solicita tipo de viagem;

:Usuário informa o tipo (curta, longa, carga, passeio etc.);

:Sistema sugere lista de itens com base no tipo e nas revisões necessárias;

:Usuário revisa e confirma checklist;

:Usuário solicita exportação;

:Sistema gera checklist em PDF;

:Usuário faz download do PDF;

stop
@enduml
```


