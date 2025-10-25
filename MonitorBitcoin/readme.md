Monitor de Alerta de Preços de Criptomoedas com n8n

Este projeto é um robô de automação ("bot") construído na plataforma low-code n8n.

O fluxo de trabalho é executado em um intervalo de tempo programado (ex: a cada hora), busca ativamente o preço atual de uma criptomoeda (Bitcoin) em uma API pública e compara esse preço com um valor-alvo pré-definido. Se o preço cair abaixo do alvo, um alerta instantâneo é enviado para um canal do Discord.

Visão Geral do Fluxo (Workflow)

Este projeto demonstra um fluxo proativo baseado em agendamento.

Funcionalidades

    Agendamento de Tarefas: O fluxo é iniciado automaticamente em um intervalo de tempo configurável (ex: a cada hora, a cada 15 minutos, etc.).

    Consumo de API Externa: Busca dados em tempo real da API pública da CoinGecko via HTTP Request.

    Lógica Condicional: Utiliza um nó IF para tomar uma decisão de negócios ("O preço está abaixo do meu alvo?").

    Notificação Seletiva: Envia um alerta (Discord) apenas se a condição for atendida, evitando spam.

Tecnologias Utilizadas

    n8n.cloud: Plataforma de automação e orquestração do fluxo.

    Schedule Trigger (Nó): Gatilho para iniciar o fluxo em intervalos de tempo fixos.

    HTTP Request (Nó): Para fazer a chamada GET à API da CoinGecko.

    IF (Nó): Para executar a lógica condicional de comparação de preços.

    Discord (Nó): Para enviar a mensagem de alerta.

Como Funciona (Detalhes do Fluxo)

    Schedule Trigger: O fluxo é iniciado automaticamente no intervalo definido (ex: a cada hora, no minuto 0).

    HTTP Request: O nó faz uma chamada GET para a API da CoinGecko (https://api.coingecko.com/api/v3/simple/price?ids=bitcoin&vs_currencies=brl) para obter o preço atual do Bitcoin em BRL.

    IF: Este nó compara o valor retornado pela API (ex: 597915) com um valor-alvo definido manualmente (ex: 550000).

    Decisão:

        Se False (Falso): O preço está acima do alvo. O fluxo termina e nada acontece.

        Se True (Verdadeiro): O preço está abaixo do alvo. O fluxo segue para o próximo passo.

    Discord: Uma mensagem de alerta formatada é enviada para um canal específico, informando o preço atual e o alvo que foi atingido.

Arquivos no Repositório

    Monitor de Alerta de Preços.json: O "código-fonte" da automação. Este arquivo pode ser importado diretamente em qualquer instância do n8n para recriar o fluxo.

Como Testar

    Faça o download do arquivo .json deste repositório.

    Importe-o para a sua instância do n8n (no canvas, vá em "Workflow" > "Import from file").

    Configure as credenciais do nó Discord (colando sua própria URL de Webhook do Discord).

    No nó IF, ajuste o Value 2 (o preço-alvo) para um valor que faça sentido para seu teste.

    Salve o fluxo.

    Para um teste imediato, clique em "Execute Workflow". Para a automação real, clique no botão para mudar de Inactive para Active.



<img width="1088" height="394" alt="image" src="https://github.com/user-attachments/assets/b0bb5774-6fee-484d-a124-77236340c28d" />


<img width="593" height="726" alt="image" src="https://github.com/user-attachments/assets/b4d10fc7-84ec-4601-bf3c-558989705f33" />
