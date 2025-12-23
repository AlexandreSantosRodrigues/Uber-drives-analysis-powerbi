🚗 Uber Drives: Um dashboard de análise de mobilidade pessoal construído com Power BI para examinar padrões de deslocamento baseados em dados reais de corridas de Uber de 2016. Este projeto transforma logs brutos de viagens em uma narrativa sobre eficiência, propósitos de viagem (Negócios vs. Pessoal) e sazonalidade.

O foco principal do projeto foi a Engenharia de Dados (ETL) e a Modelagem Dimensional, garantindo que problemas comuns de formatação de data (padrão US vs. BR) fossem resolvidos na raiz para permitir uma inteligência de tempo robusta.

📦 Tecnologias
Power BI Desktop (Visualização e Cálculos)

Power Query (M Language) (Limpeza e Padronização de Dados)

DAX (Data Analysis Expressions) (Medidas de Inteligência de Tempo e Agregação)

Modelagem Star Schema (Fato e Dimensão)

Excel/CSV (Fonte de dados)

🦄 Features
Aqui está o que você pode analisar no Uber Drives Insight:

KPIs de Eficiência: Cartões dinâmicos que mostram o Total de Milhas Percorridas, Contagem de Corridas e Duração Média (em minutos) por viagem.

Análise de Propósito: Entenda a distribuição entre viagens de Categoria "Business" vs. "Personal" e quais motivos (ex: Reunião, Aeroporto, Almoço) geram maior quilometragem.

Sazonalidade Temporal: Identifique quais dias da semana e meses do ano concentram a maior demanda de deslocamento.

Métricas de Duração Real: Cálculo preciso do tempo gasto em trânsito utilizando iteradores para analisar a diferença entre o início e fim de cada corrida.

🎯 Atalhos de Interação
Drill-down Temporal: Explore os dados navegando de Ano > Mês > Dia para encontrar outliers específicos.

Filtros Cruzados: Clique na categoria "Business" para ver automaticamente como isso afeta a duração média e os dias da semana mais utilizados.

Tooltips Informativos: Passe o mouse sobre as barras para ver detalhes específicos daquele contexto.

👩🏽‍🍳 The Process
ETL & Tratamento de Localidade (O Grande Desafio): O dataset original apresentava datas no formato americano (MM/DD/YYYY), o que gerava erros de interpretação em sistemas configurados para PT-BR. Em vez de criar colunas calculadas complexas com LEFT/MID/SEARCH, resolvi o problema na raiz usando o Power Query. Utilize o recurso "Usando a Localidade" para tipar corretamente a coluna como Data/Hora, garantindo integridade dos dados.

Modelagem Dimensional (Star Schema): Evitei o erro comum de usar uma "tabela única" (flat table). Criei uma tabela dimensão dedicada, a dCalendario, usando DAX (CALENDARAUTO, YEAR, MONTH, WEEKDAY). Isso permitiu um relacionamento 1:* limpo com a tabela fato (My Uber Drives), essencial para análises temporais corretas.

Medidas DAX Explícitas: Desenvolvi medidas para garantir cálculos dinâmicos:

Uso de AVERAGEX e DATEDIFF para calcular a duração média linha a linha, garantindo precisão no nível granular antes de tirar a média.

Medidas de contagem (COUNTROWS) e soma (SUM) organizadas em pastas de medidas.

Visualização: Ocultei colunas técnicas (como IDs e colunas de datas da tabela fato) para forçar o uso correto da tabela dimensão nos gráficos, seguindo as melhores práticas de Self-Service BI.

📚 O que eu aprendi
Este projeto reforçou conceitos fundamentais para a transição de carreira para Análise de Dados:

A importância da Tipagem de Dados: Um erro de tipo (Texto vs. Data) pode quebrar todo um modelo. Corrigir isso no Power Query é infinitamente mais performático do que criar "gambiarras" com DAX.

Iteradores (X-Functions): A diferença entre fazer uma média simples e usar AVERAGEX para iterar sobre cada corrida e calcular a duração individualmente.

Boas Práticas de Modelagem: Como a criação de uma Tabela Dimensão Calendário (dCalendario) facilita a ordenação cronológica de meses e dias da semana, evitando a ordenação alfabética incorreta.

💭 Como pode ser melhorado?
Análise Geoespacial: Integrar mapas para visualizar as rotas de partida e chegada (caso os dados de latitude/longitude estivessem disponíveis).

Cálculo de Custo Estimado: Criar parâmetros "What-If" para simular quanto teria custado essas corridas com base em tarifas médias do Uber.

Classificação Automática: Usar Grupos de Dados para categorizar viagens curtas, médias e longas automaticamente.

🚦 Executando o Projeto
Para visualizar o dashboard no seu ambiente local:

Clone este repositório ou baixe o arquivo .pbix.

Certifique-se de ter o Power BI Desktop instalado.

Abra o arquivo Uber_Drives_Analysis.pbix.

Caso necessário, vá em Transformar Dados > Configurações da Fonte de Dados e aponte para o arquivo My Uber Drives - 2016.csv na sua máquina.

🍿 Video / Dashboard em Ação

![UBER DRIVES 2016](https://github.com/user-attachments/assets/28248b89-5089-4099-839b-52ce80a9415e)
