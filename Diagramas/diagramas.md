# 📊 Diagramas UML do Sistema

## 🔹 Diagramas de Atividade

### Atividade - Cadastrar motorista
Nesse diagrama ilustra-se a atividade de cadastrar motorista, na qual o gestor da empresa pode acessar o sistema e cadastrar um
novo motorista, adicionando os seus dados.

![diag_atividade_cadmotorista](https://github.com/user-attachments/assets/5640ab74-e3f1-4191-990d-c9040ef99ac7)

### Atividade - Cadastrar frota
Nesse diagrama ilustra-se a atividade de cadastrar a frota da empresa, na qual o gestor da empresa pode acessar o sistema e
adicionar os dados para cadastro de um novo veículo.

![diag_atividade_cadfrota](https://github.com/user-attachments/assets/c8bacd2a-4801-499a-bf39-e02fdac6fe2e)

### Atividade - Cadastrar carga
Nesse diagrama ilustra-se a atividade de cadastrar uma carga, na qual o gestor da empresa pode acessar o sistema e
adicionar os dados para cadastro de uma nova carga.

![diag_atividade_cadcarga](https://github.com/user-attachments/assets/f568f886-8e6e-4f13-9c7a-1e25cf0c6ae2)

### Atividade - Alerta de licenciamento próximo ao vencimento
Nesse diagrama ilustra-se a atividade de gerar o alerta de licenciamento próximo ao vencimento, na qual o sistema, por meio de 
verificações constantes, ao verificar a proximidade do vencimento do licenciamento de um veículo da frota, emite uma mensagem
de alerta ao gestor da empresa.

![diag_atividade_alertalicenciamento](https://github.com/user-attachments/assets/1dc30612-3514-4a79-8d15-98a5442c78b6)

### Atividade - Buscar veículo
Nesse diagrama ilustra-se a atividade de buscar/filtrar veículos da frota da empresa, na qual o gestor da empresa pode acessar
o sistema, adicionar os dados do veículo requerido na busca e ter acesso ao status desse veículo.

![diag_atividade_buscarveiculo](https://github.com/user-attachments/assets/900db0df-9490-465d-a161-37bd33ff32d2)

### Atividade - Calcular média de consumo de combustível
Nesse diagrama ilustra-se a atividade de calcular a média de consumo de combustível de cada veiculo da frota,
na qual o sistema, a partir de dados de abastecimento e distância percorrida pelo veículo, calcula a sua média
de consumo e disponibiliza essa informação ao gestor da empresa.

![diag_atividade_calculacombustivel](https://github.com/user-attachments/assets/1c03d41b-1680-431a-bae6-ab9f0511bd12)

### Atividade - Empresa envia mensagem ao motorista
Nesse diagrama ilustra-se a atividade de envio de mensagem ao motorista, na qual o gestor da empresa pode acessar o sistema, no
campo correspondente, selecionar um motorista e enviar uma mensagem de texto a esse motorista.

![diag_atividade_envia_msgmotorista](https://github.com/user-attachments/assets/41d33dd7-68a6-4104-9b18-3d40d9897b2c)

### Atividade - Motorista envia mensagem para a empresa
Nesse diagrama ilustra-se a atividade de envio de mensagem para a empresa, na qual o motorista pode acessar o sistema, no campo
correspondente, escrever e enviar uma mensagem de texto para o gestor da empresa.

![diag_atividade_envia_msgempresa](https://github.com/user-attachments/assets/b81e0ecf-0461-4b2f-9947-5400680cb3f0)

### Atividade - Sugerir ponto de parada ao motorista
Nesse diagrama ilustra-se a atividade de sugestão de ponto de parada ao motorista. O sistema localiza a posição atual do motorista e verifica se há pontos de parada próximos disponíveis. Se houver, o sistema envia uma sugestão ao motorista. Caso contrário, é exibida a mensagem “Nenhum ponto próximo disponível”.

![diag_atividade_pontodescanso.png](https://github.com/user-attachments/assets/ce2af0f8-ab0d-4aea-9cf3-c2c4e9ad9d77)

### Atividade - Gerar relatório de viagem
Nesse diagrama ilustra-se a atividade de geração de relatório de viagem. O gestor ou motorista acessa o sistema, seleciona a viagem desejada e o sistema coleta os dados correspondentes. Caso os dados sejam válidos, o sistema gera um relatório detalhado e o disponibiliza. Se os dados forem inválidos, uma mensagem de erro é exibida, solicitando nova seleção da viagem.

![diag_atividade_gerarelatorio.png](https://github.com/user-attachments/assets/08709040-25fe-4338-821e-0da56fae51eb)

### Atividade -  Monitorar tempo de viagem
Nesse diagrama ilustra-se a atividade de monitoramento do tempo de viagem do motorista. A viagem se inicia e o sistema verifica continuamente se o motorista atingiu 5h30min de viagem. Caso isso ocorra, o motorista é notificado. Se ele já tiver feito uma pausa de 30 minutos, poderá continuar a viagem. Caso contrário, o sistema informa um ponto de descanso e contabiliza a pausa. Ao atingir 12h de viagem, o motorista deve descansar por 24h antes de continuar.

![Diagrama de atividade-viagem.drawio.png](https://github.com/user-attachments/assets/58f20f2e-bdaa-44fc-807b-673ec1a2c3fb)

### Atividade - Login do motorista
Nesse diagrama ilustra-se a atividade de login do motorista. O sistema exibe a tela de login e o motorista informa email e senha. Se os campos estiverem preenchidos, o sistema valida as credenciais. Se forem inválidas, uma mensagem de erro é exibida. Se forem válidas e for o primeiro acesso, o sistema solicita a troca de senha. Após isso, ou em acessos futuros, o motorista é redirecionado ao painel. Caso os campos não estejam preenchidos, o sistema solicita o preenchimento e retorna para a tela de login.

![diag_atividade_login.png](https://github.com/user-attachments/assets/8516e350-363a-48f9-a668-5524b82e67a9)

## 🔹 Diagramas de Estados
### Estados - Motorista
Nesse diagrama ilustra-se os estados que um motorista pode apresentar.

![diag_estado_motorista](https://github.com/user-attachments/assets/45c3e974-20ab-46ab-bbc5-42a115a4c538)

### Estados - Veículo
Nesse diagrama ilustra-se os estados que um veículo pode apresentar.

![diag_estado_veiculo](https://github.com/user-attachments/assets/4d41182d-e2ac-47b7-a9ee-6d544d623b8f)

### Estados - Viagem
Nesse diagrama ilustra-se os estados que uma viagem pode apresentar.

![diag_estado_viagem](https://github.com/user-attachments/assets/04e6f4c8-0204-4552-bed9-830f4a0ca5ac)

### Estados - Carga
Nesse diagrama ilustra-se os estados que uma carga pode apresentar.

![diag_estado_carga](https://github.com/user-attachments/assets/35a1c871-6199-400b-b415-09ca54c2c0e3)

### Estados - Manutenção
Nesse diagrama ilustra-se os estados que a manutenção de um veiculo pode apresentar.

![diag_estado_manutencao](https://github.com/user-attachments/assets/1bc6dffb-a033-45fe-af43-0ad191f1ab6b)

### Estados - Mensagem
Nesse diagrama ilustra-se os estados que uma mensagem pode apresentar.

![diag_estados_mensagem](https://github.com/user-attachments/assets/5a197d41-1917-4163-90a1-89242836e90d)

## 🔹 Diagrama de Classe
### Classe
Neste diagrama ilustra-se várias das classes, com seus respectivos métodos, que compõem esse Sistema.


![diagrama_classe](https://github.com/user-attachments/assets/418bb81d-e060-4722-818e-8989f884ce15)
