# Casos de Uso

## Login

**Atores Principais**: Empresa e Motoristas
**Descrição**: Permite à empresa e aos motoristas terem acesso às funcionalidades do sistema

**Fluxo Principal**:
1. O usuário vai acessar o sistema na página de login
2. O motorista irá colocar as credenciais fornecidas pela empresa
3. A empresa irá colocar a credencial de administrador fornecida pelos desenvolvedores do sistema

## Cadastro de Motorista

**Ator Principal**: Empresa
**Resumo**: Permite à empresa cadastrar novos motoristas

**Fluxo Principal**:
1. A empresa acessa o sistema
2. A empresa realiza o login com suas credenciais
3. Clica na opção de cadastro de motorista
4. O sistema exibe o formulário de cadastro
5. A empresa preenche o formulário com os dados do motorista
6. O sistema verifica se os dados são válidos e salva
7. O sistema vai retornar uma mensagem de cadastro realizado com o usuário e senha

**Fluxo Alternativo**:
1. Se algum dado não for válido ou for um dado existente de outro motorista, o sistema irá mostrar uma mensagem de erro


## Cadastro de Carga

**Ator Principal**: Empresa
**Resumo**: Permite à empresa cadastrar cargas

**Fluxo Principal**:
1. A empresa acessa o sistema
2. A empresa realiza o login com suas credenciais
3. A empresa clica na opção de cadastro de cargas
4. O sistema exibe o formulário de cadastro
5. A empresa preenche o formulário com os dados da carga
6. O sistema verifica se os dados são válidos 
7. O sistema irá retornar uma mensagem de cadastro realizado 

**Fluxo Alternativo**:
1. Se algum dado não for válido ou duplicado de outra carga, o sistema irá mostrar uma mensagem de erro


## Cadastro de Frota

**Ator Principal**: Empresa
**Resumo**: Permite à empresa cadastrar novas frotas

**Fluxo Principal**:
1. A empresa acessa o sistema
2. A empresa realiza o login com suas credenciais
3. A empresa clica na opção de cadastro de frotas
4. O sistema exibe o formulário de cadastro
5. A empresa preenche o formulário com os dados da frota
6. O sistema verifica se os dados são válidos 
7. O sistema irá retornar uma mensagem de cadastro realizado

**Fluxo Alternativo**:
1. Se existir algum dado inválido ou duplicado (como a placa do veículo), o sistema irá mostrar uma mensagem de erro


## Gerar Relatórios

**Ator Principal**: Empresa e Motorista
**Descrição**: Gera um relatório completo contendo motorista, veículo, carga, horário de saída e chegada, destino e rota

**Fluxo Principal**:
1. O usuário acessa o sistema
2. O usuário realiza o login com suas credenciais
3. O usuário seleciona a opção de relatório
4. O usuário escolhe a opção de gerar relatório
5. O sistema ira retornar um relatorio completo


## Busca

**Ator Principal**: Empresa
**Descrição**: Permite à empresa realizar uma busca por veículo, motorista ou carga

**Fluxo Principal**:
1. A empresa acessa o sistema
2. A empresa realiza o login com suas credenciais
3. Seleciona a opção de busca
4. Filtra qual item quer buscar
5. O sistema retorna a busca baseada no filtro

**Fluxo Alternativo**:
1. A busca por veiculo ira retornar uma lista com os veiculos que estao disponiveis e ocupados
2. No resultado da busca de veiculos ocupados, sera retornado os motoristas e as cargas vinculadas


## Envio de Mensagens

**Atores Principais**: Empresa e Motoristas
**Descrição**: Permite a comunicação escrita entre empresa e motorista

**Fluxo Principal**: 
1. O usuário vai acessar o sistema
2. O usuário vai logar no sistema
3. O usuário vai selecionar a opção de mensagens
4. O usuário seleciona para quem deseja enviar a mensagem ou ver as recebidas


## Multas

**Ator Principal**: Empresa
**Descrição**: Permite à empresa ver as multas dos veículos

**Fluxo Principal**:
1. A empresa vai acessar o sistema
2. A empresa realiza o login com suas credenciais
3. A empresa seleciona a opção de multas
4. O sistema irá retornar todos os veículos que estão com multa
5. A empresa irá direcionar a multa para o motorista responsável

**Fluxo Alternativo**:
1. Se não houver motorista cadastrado para direcionar a multa, o sistema irá mostrar uma mensagem de erro


## Licenciamento

**Ator Principal**: Empresa
**Descrição**: A empresa acompanha os licenciamentos dos veículos

**Fluxo Principal**: 
1. A empresa acessa o sistema
2. A empresa realiza o login com suas credenciais
3. A empresa seleciona a opção de licenciamento
4. O sistema irá retornar o licenciamento de todos os veículos e as datas de pagamento
5. O sistema irá notificar quando estiver próximo à data de pagamento do licenciamento

**Fluxo Alternativo**:
1. Se não houver veículos cadastrados no sistema, será mostrada uma mensagem informando que não há veículos para exibir


## Limite de Tempo

**Ator Principal**: Motorista
**Descrição**: Notifica o motorista sobre o tempo limite de serviço de descanso para a pausa de 30 min e o descanso de 24H

**Fluxo Principal**:
1. O motorista irá acessar o sistema
2. O motorista irá realizar o login com suas credenciais
3. O sistema irá notificar o motorista caso ele atinja os limites determinados pela empresa


## Pontos de Descanso

**Ator Principal**: Motorista
**Resumo**: Notifica o motorista quando existirem pontos de descanso próximos

**Fluxo Principal**:
1. O motorista irá acessar o sistema
2. O motorista irá realizar o login com suas credenciais 
3. O sistema irá notificar quando tiver algum ponto de descanso por perto

**Fluxo Alternativo**:
1. Se não houver pontos de descanso cadastrados na região, o sistema informará que não há pontos próximos


## Monitorar Km

**Ator Principal**: Motorista
**Descrição**: Permite ao motorista ver quantos quilômetros foram percorridos do ponto de origem até o destino, quanto falta para chegar e monitorar a velocidade atual

**Fluxo Principal**:
1. O motorista irá acessar o sistema
2. O motorista irá realizar o login com suas credenciais 
3. O motorista irá para a tela de viagem
4. O sistema irá mostrar a quilometragem total, quanto foi percorrido, quanto está faltando e a velocidade atual do veículo
5. O sistema irá alertar caso a velocidade ultrapasse o limite permitido

**Fluxo Alternativo**:
1. Se não houver viagem em andamento ou dados de rota cadastrados, o sistema irá mostrar uma mensagem de erro
2. Se o GPS estiver desativado, o sistema solicitará a ativação para continuar o monitoramento


## Média de Combustível

**Ator Principal**: Empresa
**Descrição**: Permite à empresa ter uma média de Km/L que o veículo irá fazer para estimar o quanto vai ser gasto de combustível, além de manter um histórico de consumo

**Fluxo Principal**:
1. A empresa acessa o sistema
2. A empresa realiza o login com suas credenciais
3. A empresa irá apertar o botão de cálculo de média
4. O sistema irá pedir as informações de origem, destino e modelo do veículo
5. A empresa preenche todas as informações
6. O sistema calcula e informa uma média de consumo baseada nas informações fornecidas
7. O sistema exibe um histórico comparativo de consumo do veículo

**Fluxo Alternativo**:
1. Se alguma informação estiver faltando ou for inválida, o sistema irá mostrar uma mensagem de erro solicitando o preenchimento correto
2. Se não houver histórico anterior para comparação, o sistema informará que é a primeira medição
