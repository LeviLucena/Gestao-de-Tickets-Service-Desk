# Dashboards de Service Desk no Grafana

Este projeto consiste em uma coleção de dashboards no Grafana para monitorar e visualizar métricas relacionadas a um sistema de chamados do Service Desk, utilizando consultas no banco de dados PostgreSQL.

## Requisitos
Grafana (versão X.X.X)
Banco de dados PostgreSQL (versão X.X.X)

![Dashboard Grafana](https://github.com/LeviLucena/Gestao-de-Tickets-Service-Desk/assets/34045910/25822040-f0d6-4f72-8f79-0cc5369b0f02)

## Instalação
Clone este repositório em sua máquina local:

    bash

    git clone https://github.com/LeviLucena/Gestao-de-Tickets-Service-Desk.git

### Importe os dashboards no Grafana:
1. Acesse o Grafana e faça login.
2. Navegue até o painel do Grafana.
3. No menu esquerdo, clique em "Create" e selecione "Import".
4. No campo "Upload .json File", selecione os arquivos .json dos dashboards que deseja importar, localizados na pasta dashboards/ do repositório clonado.
5. Clique em "Load" para carregar os dashboards.
6. Faça as configurações necessárias (por exemplo, selecione a fonte de dados correta) e clique em "Import".

### Configuração da fonte de dados PostgreSQL:
7. Certifique-se de que a fonte de dados PostgreSQL esteja configurada corretamente no Grafana.
8. No Grafana, navegue até o menu de configurações (ícone de engrenagem no canto superior direito) e selecione "Data Sources".
9. Clique em "Add data source" e selecione "PostgreSQL".
10. Preencha os detalhes de conexão com o banco de dados PostgreSQL (como endereço, porta, nome do banco de dados, usuário e senha).
11. Teste a conexão para verificar se está funcionando corretamente e, em seguida, clique em "Save & Test" para salvar a fonte de dados.

### Configuração das consultas:
12. Abra cada dashboard importado no Grafana e clique em "Edit" para editar as consultas.
13. Certifique-se de que as consultas estejam apontando para a fonte de dados PostgreSQL correta e ajuste as consultas, se necessário, para corresponder ao esquema do banco de dados em uso.
14. Salve as alterações após fazer os ajustes necessários.

### Personalização e configuração adicional:
15. Você pode personalizar e ajustar os dashboards conforme suas necessidades específicas, adicionando painéis, métricas adicionais, filtros, alertas, etc.

## Uso
Após a conclusão da instalação e configuração, você poderá acessar os dashboards no Grafana para monitorar as métricas do sistema de chamados do Service Desk.

Os dashboards incluídos neste projeto:

- Tickets Abertos: Exibe o número total de tickets abertos nos últimos 21 horas.
   SELECT COUNT(distinct t.id) FROM ticket t WHERE t.create_time > now() - interval '21 hours' AND queue_id IN (12,14,15,16,17,18,19,44,45,55,56) AND t.ticket_state_id in (1,12,13,18,21,22,25);
  
- Tickets Fechados: Exibe o número total de tickets fechados nos últimos 21 horas.
   SELECT COUNT(distinct t.id) FROM ticket t, ticket_history th WHERE t.id = th.ticket_id AND t.create_time > now() - interval '21 hours' AND t.queue_id IN (12,14,15,16,17,18,19,44,45,55,56) AND t.ticket_state_id in (11,17,19,20,23,24);
  
- Tickets por Prioridade: Exibe a contagem de tickets abertos agrupados por prioridade.
  SELECT NOW() AS Time, ticket_priority.name, COUNT(*) AS " " FROM ticket_priority INNER JOIN ticket ON ticket_priority.id = ticket.ticket_priority_id WHERE queue_id IN (12,14,15,16,17,18,19,44,45,50,55,56) AND ticket_state_id in (1,12,13,18,21,22,25) GROUP BY ticket_priority.name, 1 ORDER BY 3 DESC, 1;
  
- Tickets Abertos por Tipo: Exibe a contagem de tickets abertos agrupados por tipo.
  SELECT tt.name AS Tipo, COUNT(t.tn) AS Qtd FROM ticket t INNER JOIN ticket_type tt ON t.type_id = tt.id WHERE t.create_time > now() - interval '21 hours' GROUP BY tt.name ORDER BY Qtd DESC;
  
- Tickets Abertos por Estado: Exibe a contagem de tickets abertos agrupados por estado.
  SELECT ts.name AS ESTADO, COUNT(*) AS total FROM ticket t LEFT JOIN ticket_state ts ON ts.id = t.ticket_state_id WHERE t.ticket_state_id IN (12,13,18,21,22,25) AND queue_id IN (12,14,15,16,17,18,19,44,45,55,56) GROUP BY 1 ORDER BY 2 DESC;
  
- Tickets Fechados por Estado: Exibe a contagem de tickets fechados agrupados por estado.
  SELECT ts.name AS ESTADO, COUNT(*) AS total FROM ticket t LEFT JOIN ticket_state ts ON ts.id = t.ticket_state_id WHERE t.ticket_state_id IN (11,17,19,20,23,24) AND queue_id IN (12,14,15,16,17,18,19,44,45,55,56) AND t.create_time > NOW() - interval '21 hours' GROUP BY 1 ORDER BY 2 DESC;
  
- Tickets Sem Atendente: Exibe o número total de tickets abertos sem atendente nos últimos 21 horas.
  SELECT COUNT(*) FROM ticket t WHERE user_id = 1 AND t.create_time > now() - interval '21 hours' AND queue_id IN (12,14,15,16,17,18,19,44,45,55,56)
  
- Tickets por Analista: Exibe a contagem de tickets abertos por analista.
  SELECT Users.first_name AS Nome,Users.last_name AS Sobrenome, COUNT(ticket.user_id) AS Total FROM ticket INNER JOIN Users ON ticket.user_id = Users.id WHERE ticket.user_id In (119,159,249,270,279,283,285,291,295,297) AND queue_id IN (12,14,15,16,17,18,19,44,45,55,56) AND ticket_state_id in (1,12,13,18,21,22,25) GROUP BY ticket.user_id, users.first_name, users.last_name ORDER BY users.first_name asc;
  
- Tickets Abertos por Período: Exibe a contagem de tickets abertos por dia.
  SELECT DATE(ticket.create_time) AS "Date", COUNT(ticket.id) AS "# of tickets" FROM ticket INNER JOIN queue ON ticket.queue_id = queue.id WHERE ticket.queue_id IN (SELECT id FROM queue WHERE valid_id = 1 ORDER BY name) GROUP BY DATE(ticket.create_time);
  
- Tickets Abertos por Fila: Exibe a contagem de tickets abertos por fila.
  SELECT NOW() AS Time, queue.name AS FILA, COUNT(*) AS " " FROM ticket INNER JOIN queue ON ticket.queue_id = queue.id WHERE queue_id IN (12,14,15,16,17,18,19,44,45,56) AND ticket_state_id IN (12,13,25,21,18,22) GROUP BY queue.name, 1 ORDER BY 3 DESC, 1;
  
- Tickets Recentes: Exibe uma lista de tickets abertos recentemente, incluindo detalhes como título, fila, analista responsável, status e e-mail do cliente.
  SELECT t.tn AS Ticket, t.title AS Título, q.name AS Fila, u.login AS Analista, ts.name AS Status, t.customer_id AS Email FROM ticket t LEFT JOIN queue q ON t.queue_id=q.id LEFT JOIN users u ON t.user_id = u.id LEFT JOIN ticket_state ts ON ts.id = t.ticket_state_id WHERE queue_id in (12,14,15,16,17,18,19,44,45,50,55,56) and t.create_time > now() - interval '21 hours';

## Contribuição
Este projeto está licenciado sob a MIT License, Se você deseja contribuir para este projeto, sinta-se à vontade para fazer um fork, implementar melhorias e enviar um pull request.
Licença

Espero que isso te ajude a criar o README do seu projeto de Dashboards Service Desk no Grafana. Lembre-se de ajustar as instruções de acordo com o seu ambiente específico.
