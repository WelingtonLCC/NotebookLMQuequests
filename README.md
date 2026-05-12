# NotebookLMQuequests
Requests demoradas
Escalonamento de APIs com Requisições de Longa Duração
Este guia descreve a evolução arquitetural para lidar com APIs que realizam tarefas demoradas (como geração de relatórios ou processamento de arquivos pesados) sem comprometer a experiência do usuário ou a estabilidade do servidor
.
🚀 Problemas Identificados
Má experiência do usuário: Esperas de vários minutos por uma resposta síncrona
.
Instabilidade do servidor: Requisições abertas por muito tempo consomem recursos e limitam a capacidade de lidar com novos acessos
.
🏗️ Evolução da Solução
1. API Assíncrona (Padrão Job-Table)
Resposta Imediata: A API retorna um código 202 Accepted assim que recebe a solicitação
.
Persistência: O trabalho é registrado em uma tabela de "jobs" no banco de dados
.
Processamento em Background: Um componente separado busca e executa as tarefas pendentes fora do fluxo principal
.
2. Desacoplamento com Filas (Messaging)
Buffer de Mensagens: Introdução de uma fila (Queue) para mediar a comunicação entre a API e os processadores
.
Consumidores Concorrentes: Uso de múltiplas instâncias de processadores trabalhando em paralelo para escalar a vazão do sistema
.
3. Resiliência e Notificações
Tratamento de Erros: Implementação de retentativas automáticas e Dead Letter Queues (DLQ) para falhas persistentes
.
Status: O usuário acompanha o progresso via Polling (consultas periódicas) ou notificações em tempo real usando WebSockets, SSE ou E-mail
.
🔗 Links Relacionados
Notebook desta conversa: Acesse aqui
