Esta célula documenta objetivos, arquitetura, metodologia, execução, limitações e uso responsável. Use-a como célula de texto/Markdown no Colab.
# Previsão de PM2.5 e Risco à Saúde em Grandes Cidades Brasileiras

Pipeline completo de Machine Learning para prever concentrações horárias de material particulado fino (PM2.5) e classificar o risco à saúde pública nas próximas 24 horas.

O projeto utiliza dados públicos atuais, validação específica para séries temporais, modelos de regressão e classificação, otimização de hiperparâmetros, interpretabilidade com SHAP e geração de alertas operacionais.

## Objetivos

- Coletar dados atuais de poluição atmosférica e meteorologia.
- Prever PM2.5 para cada horizonte entre 1 e 24 horas.
- Classificar o risco em baixo, médio ou alto.
- Identificar antecipadamente possíveis picos de poluição.
- Produzir informações úteis para alertas de saúde e políticas públicas.
- Demonstrar um pipeline de Data Science reproduzível e executável no Google Colab.

## Cidades monitoradas

| Cidade | Estado/DF |
|---|---|
| São Paulo | SP |
| Rio de Janeiro | RJ |
| Brasília | DF |
| Belo Horizonte | MG |
| Salvador | BA |
| Fortaleza | CE |
| Recife | PE |
| Manaus | AM |
| Curitiba | PR |
| Porto Alegre | RS |

As coordenadas utilizadas representam pontos centrais das cidades. Os dados atmosféricos têm resolução espacial em grade e não correspondem necessariamente a uma estação de monitoramento específica.

## Fontes de dados

### Open-Meteo Air Quality API

Variáveis coletadas:

- PM2.5
- PM10
- Dióxido de nitrogênio
- Ozônio
- Monóxido de carbono
- Dióxido de enxofre

### Open-Meteo Weather API

Variáveis coletadas:

- Temperatura
- Umidade relativa
- Precipitação
- Pressão atmosférica
- Cobertura de nuvens
- Velocidade do vento
- Direção do vento

As consultas possuem timeout, validação das respostas, retentativas automáticas e tratamento explícito de falhas de conexão.

## Arquitetura do pipeline

```text
APIs públicas
     |
     v
Coleta e validação
     |
     v
Limpeza e auditoria
     |
     v
EDA temporal e espacial
     |
     v
Feature engineering causal
     |
     v
Validação temporal
     |
     +-------------------+
     |                   |
     v                   v
Regressão PM2.5    Classificação de risco
     |                   |
     +---------+---------+
               |
               v
      SHAP e análise de erros
               |
               v
       Previsão operacional
               |
               v
 Alertas, dashboard e monitoramento
Engenharia de atributos
O pipeline cria atributos capazes de representar persistência, tendência, sazonalidade e condições meteorológicas.
Atributos temporais
- Hora local
- Dia da semana
- Mês
- Dia do ano
- Indicador de final de semana
- Codificação cíclica com seno e cosseno
- Hora e dia da semana do horizonte previsto
Histórico de PM2.5
- Lags de 1, 3, 6, 12, 24, 48, 72 e 168 horas
- Médias móveis de 3, 6, 12, 24, 72 e 168 horas
- Desvios-padrão móveis
- Mudanças nas últimas 3 e 24 horas
- Razão entre PM2.5 e PM10
- Indicadores robustos de concentrações extremas
Meteorologia e poluentes
- Temperatura e suas tendências
- Umidade relativa e suas tendências
- Precipitação
- Pressão
- Cobertura de nuvens
- Velocidade do vento
- Direção do vento em representação circular
- Concentração dos demais poluentes
Todas as features históricas são calculadas de maneira causal, utilizando somente informações disponíveis no momento de origem da previsão.
Definição operacional de risco
Nível
Baixo
Médio
Alto
Essas faixas são utilizadas para fins analíticos neste projeto. Elas não substituem índices oficiais de qualidade do ar, orientações médicas ou protocolos definidos pelas autoridades sanitárias.
Modelos
Persistência
Baseline que assume que a concentração futura permanecerá igual à concentração atual.
Random Forest
Modelo de referência baseado em árvores, capaz de representar relações não lineares e interações entre poluição, clima e atributos temporais.
XGBoost
Modelo avançado de regressão otimizado com Optuna. Produz previsões de PM2.5 para horizontes entre 1 e 24 horas.
XGBoost Classifier
Modelo multiclasse dedicado à previsão do risco. Utiliza pesos balanceados para aumentar a atenção às classes menos frequentes, especialmente episódios de risco alto.
Validação temporal
Divisões aleatórias não são utilizadas, pois permitiriam que informações futuras influenciassem o treinamento.
A estratégia inclui:
- Holdout com os 14 dias mais recentes.
- Quatro folds de validação temporal.
- Sete dias de validação em cada fold.
- Intervalo de segurança de 24 horas entre treino e validação.
- Agrupamento de cidades e horizontes pertencentes ao mesmo instante.
- Pré-processamento ajustado separadamente em cada fold.
O intervalo de segurança evita que alvos de até 24 horas do conjunto de treino alcancem o período de validação.
Métricas
Regressão
- MAE
- RMSE
- R²
- Erro por horizonte
- Erro por cidade
- Viés de previsão
- Taxa de subestimação
Classificação
- Accuracy
- Balanced Accuracy
- F1 macro
- F1 ponderado
- ROC-AUC multiclasse
- Precision e recall por classe
- Matriz de confusão
Os resultados são calculados durante a execução do notebook porque dependem da data da consulta e das respostas atuais das APIs.
Otimização
O Optuna pesquisa hiperparâmetros como:
- Learning rate
- Profundidade máxima
- Peso mínimo por nó
- Subsample
- Proporção de atributos por árvore
- Regularização L1 e L2
- Gamma
A função objetivo minimiza o MAE médio nos folds temporais. Early stopping e pruning reduzem treinamentos desnecessários.
Interpretabilidade
O SHAP é utilizado para explicar o comportamento do XGBoost.
O notebook inclui:
- Importância global dos atributos.
- Direção dos impactos sobre as previsões.
- Gráfico beeswarm.
- Explicação local do alerta mais severo.
- Waterfall plot para detalhar contribuições positivas e negativas.
Previsão operacional
Para cada cidade, o pipeline produz:
- 24 previsões horárias de PM2.5.
- Classe prevista de risco.
- Probabilidades de risco baixo, médio e alto.
- Confiança do classificador.
- Horário local do possível pico.
- Recomendação de saúde associada.
- Intervalo empírico de incerteza.
A regra operacional adota o nível mais severo entre a classificação probabilística e a classificação baseada na concentração prevista.
Dashboard
O painel interativo permite:
- Selecionar uma cidade.
- Visualizar as próximas 24 horas.
- Comparar a previsão com os limites de risco.
- Acompanhar probabilidades por classe.
- Identificar horários com maior concentração.
- Examinar intervalos de incerteza.
Monitoramento de drift
O Population Stability Index, ou PSI, compara os sete dias mais recentes com o histórico de referência.
PSI
Menor que 0,10
Entre 0,10 e 0,25
Acima de 0,25
Drift elevado não comprova falha do modelo, mas indica necessidade de investigação, nova validação e possível retreinamento.
Recomendações para políticas públicas
1. Atualizar previsões e alertas em frequência horária.
2. Integrar o pipeline a painéis municipais de qualidade do ar.
3. Priorizar crianças, idosos, gestantes e pessoas com doenças respiratórias ou cardiovasculares.
4. Comunicar preventivamente aumentos na probabilidade de risco alto.
5. Avaliar restrições temporárias a queimadas, obras com poeira e tráfego pesado durante episódios severos.
6. Combinar as previsões com estações regulatórias antes da emissão de alertas oficiais.
7. Monitorar recall de risco alto, erros por cidade e drift dos atributos.
8. Recalibrar os modelos e intervalos de incerteza periodicamente.
Limitações
- Os dados de qualidade do ar são estimativas atmosféricas em grade.
- As estimativas não substituem estações regulatórias em superfície.
- O histórico recente não representa toda a sazonalidade anual.
- Eventos como incêndios, queimadas, obras e alterações de tráfego não são modelados diretamente.
- Não há arquivos históricos das previsões meteorológicas emitidas em cada instante.
- Os intervalos de incerteza são empíricos e precisam de validação futura.
- As probabilidades não representam certeza clínica.
- Mudanças climáticas, urbanas ou na fonte de dados podem degradar o desempenho.
- Os limites de risco usados pelo projeto são operacionais, não diagnósticos.
Execução
O projeto foi desenvolvido para rodar integralmente em células do Google Colab.
Ordem recomendada:
Etapa
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
Nenhuma estrutura local de diretórios é necessária. Os dados, modelos, previsões e relatórios permanecem em memória durante a sessão.
Tecnologias
- Python
- pandas
- NumPy
- requests
- scikit-learn
- XGBoost
- Optuna
- SHAP
- Plotly
- Matplotlib
- Seaborn
- Google Colab
Reprodutibilidade
O projeto utiliza seed global fixa:
SEED = 42
Os resultados ainda podem variar devido a:
- Atualização contínua dos dados das APIs.
- Alterações nas versões das bibliotecas.
- Mudanças nas estimativas dos modelos atmosféricos.
- Paralelização interna dos algoritmos.
Uso responsável
Este projeto é uma ferramenta analítica e educacional. Suas previsões não devem ser utilizadas isoladamente para decisões médicas, regulatórias ou emergenciais.
Alertas oficiais devem combinar:
- Estações de monitoramento certificadas.
- Avaliação de especialistas ambientais.
- Protocolos das autoridades sanitárias.
- Evidências meteorológicas e epidemiológicas.
- Comunicação clara da incerteza.
