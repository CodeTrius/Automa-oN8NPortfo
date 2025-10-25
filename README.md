# Projetos de Automação com n8n

Este repositório armazena uma coleção de fluxos de trabalho (workflows) criados na plataforma de automação *low-code* n8n. Cada subpasta contém o JSON de um workflow específico, demonstrando diferentes gatilhos, integrações e lógicas de negócio.

#Workflows

# 1. Api de Leads (Formulário para Discord e Google Sheets)

* Arquivo: 'FormularioAvisoDIscord.json'
* Propósito: Automatizar o processo de captura de leads de um formulário web.
* Gatilho: 'Webhook' - Aguarda dados enviados via 'POST'.
* Fluxo:
    1.  Webhook: Recebe os dados do lead (nome, email, telefone).
    2.  Set: Formata os dados recebidos. (aplica '.toTitleCase()' ao nome e trata valores nulos).
    3.  Google Sheets: Adiciona uma nova linha à planilha com os dados do lead (Nome, Email, Telefone) e um timestamp ('Data de Registro').
    4.  Discord: Envia uma mensagem formatada para um canal específico, notificando sobre o novo lead.
    5.  Respond to Webhook: Retorna uma resposta (Pode-ser qualquer tipo de mensagem : (Exemplo: ,"Ola")) para a requisição original.

### 2. Monitor de Alerta de Preços (Bitcoin)

* Arquivo: 'Monitor de Alerta de Preços.json'
* Propósito: Monitorar o preço de um ativo (Bitcoin) e enviar um alerta caso atinja uma condição específica.
* Gatilho: 'Schedule Trigger' - Executa o workflow a cada 1 minuto.
* Fluxo:
    1.  HTTP Request: Faz uma chamada 'GET' à API do CoinGecko ('api.coingecko.com') para obter o preço atual do Bitcoin em BRL.
    2.  If: Verifica se o valor retornado ('$json.bitcoin.brl') é menor que '600000'.
    3.  Discord (Condicional): Se a condição for verdadeira (preço abaixo de R$ 600.000), envia uma mensagem de alerta para um canal do Discord.
