# lives.Compras

Neste repositório você encontra o processo de compras apresentado na live do dia 8 de outubro de 2020, disponível no link abaixo:
https://www.youtube.com/watch?v=a7oYi9ycv34
Trata-se de um processo de controle de pedido de compras.

## O que este pacote faz?
* Disponibiliza um processo de controle de pedidos de compras como processo Read2Adopt, dentro do Gerenciador de Processos do LigeroSmart
* Cria a fila "Compras"
* Cria os estados "Aguardando aprovação Gerência", "Cotação Concluída", "Em Cotação" e "Requisição Cancelada"

## Instalação do Processo
Primeiramente: realize o teste deste processo em um servidor de homologação!
Para instalar em seu LigeroSmart, acesse Administração -> Gerenciamento de Pacotes.
Instale o OPM disponível neste repositório Git.
Em seguida, acesse Administração -> Gerenciamento de Processos. Do lado esquerdo da tela, você encontrará uma caixa chamada "Processos Ready2Adopt".
Selecione PedidoDeCompras e clique em "Importar processos Ready2Adopt".
O processo foi importado, mas ainda precisa clicar em "Implantar todos os processos" para que ele apareça na lista de novos chamados de processo.
Verifique se não é necessário realizar a implantação também de novas configurações de sistema, acessando Administração --> Configurações do Sistema.

### Configuração das Aprovações
Parte deste processo requer a aprovação de uma área para continuidade no andamento do pedido de Compras. Isto deve ser configurado de acordo com a estrutura de sua empresa.
Crie uma fila para cada aprovador. Possívelmente, você terá uma por departamento, mais ou menos assim:
* Aprovadores RH
* Aprovadores TI
* Aprovadores Logística
* Aprovadores XXXXXX...

### Atendentes Genéricos de Aprovação
O chamado deverá ser colocado nestas filas, quando ocorrer a atualização do estado do chamado para "Aguardando aprovação Gerência", de acordo com o ID do Cliente. O ID do Cliente neste caso seria o setor onde trabalha.
Para isso ocorrer então, você deverá criar alguns atendentes genéricos, de acordo com as possíveis situações de encaminhamento. Exemplos:

##### Nome: 001 - Aprovações RH
Execução Baseada Em Evento:
* Tipo "Ticket", Evento "TicketStateUpdate"

Selecionar Chamados:
* ID do Cliente: Escreva o ID dos clientes que devem ter suas solicitações aprovadas pela área de RH
* Serviço: Aqui selecione os serviços que devem ser encaminhados para a fila de Aprovação
* Estado: Aguardando aprovação da Gerência

Alterar/Adicionar Atributos do Chamado
* Configurar Nova Fila: "Aprovadores RH"

Com a criação deste atendente genérico, todas as solicitações que requerem aprovação da área de RH (usuários do departamento RH e chamados que requerem aprovação) serão encaminhados para a fila "Aprovadores RH"

Você deverá criar também Atendentes Genéricos para as demais áreas (ID de Cliente) de sua empresa, seguindo o mesmo padrão.

#### IMPORTANTE
O chamado retorna automaticamente para a fila "Compras" quando é aprovado ou reprovado (cancelado). Se você deseja alterar esse comportamento, deve alterar então o processo, criando novas ações de transição para mover para outras filas de seu interesse. Para isso, você irá precisar de algum conhecimento de Gerenciamento de Processos.
