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
- Tickets Fechados: Exibe o número total de tickets fechados nos últimos 21 horas.
- Tickets por Prioridade: Exibe a contagem de tickets abertos agrupados por prioridade.
- Tickets Abertos por Tipo: Exibe a contagem de tickets abertos agrupados por tipo.
- Tickets Abertos por Estado: Exibe a contagem de tickets abertos agrupados por estado.
- Tickets Fechados por Estado: Exibe a contagem de tickets fechados agrupados por estado.
- Tickets Sem Atendente: Exibe o número total de tickets abertos sem atendente nos últimos 21 horas.
- Tickets por Analista: Exibe a contagem de tickets abertos por analista.
- Tickets Abertos por Período: Exibe a contagem de tickets abertos por dia.
- Tickets Abertos por Fila: Exibe a contagem de tickets abertos por fila.
- Tickets Recentes: Exibe uma lista de tickets abertos recentemente, incluindo detalhes como título, fila, analista responsável, status e e-mail do cliente.

## Contribuição
Este projeto está licenciado sob a MIT License, Se você deseja contribuir para este projeto, sinta-se à vontade para fazer um fork, implementar melhorias e enviar um pull request.
Licença

Espero que isso te ajude a criar o README do seu projeto de Dashboards Service Desk no Grafana. Lembre-se de ajustar as instruções de acordo com o seu ambiente específico.
