Sincronização de Leads com n8n (Webhook > Google Sheets > Discord)"

Descrição: Este projeto é um fluxo de automação ETL construído em n8n que captura leads de um formulário web, limpa os dados, salva-os em uma planilha Google e envia uma notificação em tempo real para o Discord.

Automação de Captura de Leads com n8n

Este projeto demonstra um pipeline de automação (ETL) para captura e processamento de leads, construído inteiramente na plataforma low-code n8n.

O objetivo é criar um endpoint de API (Webhook) que recebe dados de um formulário HTML, executa a limpeza e formatação desses dados, e os distribui para um banco de dados (Google Sheets) e um sistema de notificação (Discord) simultaneamente.

Visão Geral do Fluxo (Workflow)

Funcionalidades

    Endpoint de API em Tempo Real: Recebe dados via POST de qualquer formulário web.

    Limpeza e Transformação (ETL): Formata os dados recebidos (ex: transforma "joão silva" em "João Silva") e é robusto o suficiente para aceitar dados de teste (query params) ou de produção (body).

    Persistência de Dados: Salva cada novo lead como uma nova linha em uma planilha do Google Sheets, que atua como banco de dados.

    Notificação Instantânea: Envia uma mensagem formatada para um canal do Discord no exato momento em que o lead é capturado.

    Execução Paralela: As ações de salvar no Google Sheets e notificar no Discord ocorrem ao mesmo tempo para máxima eficiência.

Tecnologias Utilizadas

    n8n.cloud: Plataforma de automação e orquestração do fluxo.

    Webhook: Nó de gatilho que expõe uma URL pública.

    Google Sheets: Utilizado como banco de dados para armazenar os leads.

    Discord: Utilizado para enviar notificações em tempo real.

    HTML5: O formulário (index.html) que simula a fonte externa dos leads.

Como Funciona

O fluxo de trabalho é iniciado quando uma requisição POST é enviada para a URL de produção do Webhook.

    Formulário HTML: O usuário preenche o index.html com Nome, Email e Telefone. Ao clicar em "Enviar", os dados são enviados para a URL do n8n.

    Webhook (Nó): Recebe os dados.

    Recebe a variavel manual (Nó Set): Este nó de transformação executa duas funções:

        Extrai os dados de $json.body (do formulário) ou $json.query (de testes de URL).

        Limpa e formata os dados, por exemplo, usando {{ $json.Nome.toTitleCase() }} para padronizar o nome.

    Divisão do Fluxo (Execução Paralela):

        Ramo A: Atualiza Google Sheets: Utiliza a operação append para adicionar uma nova linha na planilha com os dados do lead e a data/hora do registro (usando {{ $now }}).

        Ramo B: Discord: Formata e envia uma mensagem para um canal específico, notificando a equipe sobre o novo lead.

Arquivos no Repositório

    [NomeDoSeuFluxo].json: O "código-fonte" da automação. Este arquivo pode ser importado diretamente em qualquer instância do n8n para recriar o fluxo.

    index.html: Um formulário web estático usado para testar o endpoint.

Como Testar

    Faça o download do arquivo .json deste repositório.

    Importe-o para a sua instância do n8n (no canvas, vá em "Workflow" > "Import from file").

    Configure as credenciais (OAuth2 para Google Sheets e Webhook URL para Discord).

    Ative o fluxo (clicando no botão Active no canto superior direito).

    Copie a Production URL do seu nó Webhook.

    Abra o arquivo index.html e cole a sua URL no campo action="" do formulário.

    Abra o index.html no seu navegador, preencha os dados e clique em "Enviar".

    Verifique sua planilha e seu canal do Discord!

<img width="1288" height="320" alt="image" src="https://github.com/user-attachments/assets/09d1abe5-ed88-4e92-a3e0-22a6248b7d84" />


<img width="1065" height="460" alt="image" src="https://github.com/user-attachments/assets/8f40d1eb-0151-4ead-bce6-6892dfbaa07b" />


<img width="398" height="826" alt="image" src="https://github.com/user-attachments/assets/22a2cc8b-4ccb-4ded-a44e-737384cccb17" />

<img width="419" height="693" alt="image" src="https://github.com/user-attachments/assets/f3dbac60-2f65-4be8-80fd-f86e04a115f8" />

