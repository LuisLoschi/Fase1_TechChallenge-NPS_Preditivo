# 📊 [FIAP - Fase1] Tech Challenge: Case NPS Preditivo

![Data Science](https://img.shields.io/badge/Area-Data%20Science-blue)
![Python](https://img.shields.io/badge/Language-Python-blue)
![Static Badge](https://img.shields.io/badge/Status-Done-green)

Grupo: Eduardo Rossi | Luis Loschi | Luiza Santos | Vitória Santos | Vyctor Correia

## 📌 Sumário
- [Objetivo do Projeto](#objetivo-do-projeto)
- [Problema do Negócio](#problema-do-negocio)
- [Descrição da base de dados](#descricao-da-base-de-dados)
- [Estrutura do Repositório](#estrutura-do-repositorio)
- [Entrega Executiva](#entrega-executiva)
- [Metodologia e Desenvolvimento](#metodologia-e-desenvolvimento)
- [Principais análises realizadas](#principais-analises-realizadas)
- [Cuidados contra data leakage](#cuidados-contra-data-leakage)
- [Modelos preditivos](#modelos-preditivos)
- [Como Reproduzir o Projeto](#como-reproduzir-o-projeto)
- [Como usar os modelos treinados](#como-usar-os-modelos-treinados)
- [Principais insights de negócio](#principais-insights-de-negocio)
- [Recomendações de negócio](#recomendacoes-de-negocio)
- [Limitações](#limitacoes)
- [Próximos passos](#proximos-passos)
- [Resumo executivo](#resumo-executivo)

<a id="objetivo-do-projeto"></a>
## 🎯 Objetivo do Projeto
Desenvolver uma análise completa de **NPS preditivo** para um e-commerce fictício, utilizando dados históricos de pedidos, entregas e atendimento para identificar os principais fatores associados à satisfação do cliente e construir modelos capazes de apoiar ações preventivas antes da aplicação da pesquisa de NPS.

O projeto busca transformar dados operacionais em um sistema de alerta para risco de detratação, permitindo que áreas como CX, logística, atendimento e negócio priorizem clientes com maior probabilidade de insatisfação.

O foco principal é o **Storytelling com Dados**: traduzir métricas técnicas em recomendações estratégicas para a empresa.

<a id="problema-do-negocio"></a>
## 🔎 Problema do Negócio

O NPS costuma ser conhecido apenas depois que a experiência de compra foi encerrada. Isso torna a gestão de CX predominantemente reativa: a empresa descobre que o cliente está insatisfeito quando a oportunidade de recuperação da experiência já pode ter diminuído.

Este projeto responde à seguinte pergunta:

> Quais sinais operacionais permitem antecipar baixa satisfação e apoiar ações preventivas antes da aplicação da pesquisa NPS?

A proposta é usar variáveis observáveis ao longo da jornada do pedido para estimar risco de insatisfação e orientar decisões práticas de logística, atendimento e relacionamento com o cliente.

<a id="descricao-da-base-de-dados"></a>
## 📝 Descrição da base de dados

A base `data/desafio_nps_fase_1.csv` possui **2.500 registros** e **19 colunas**.

As variáveis cobrem informações de:

- perfil do cliente;
- pedido;
- entrega;
- frete;
- atendimento;
- reclamações;
- recompra;
- CSAT interno;
- NPS.

A variável alvo principal é:

- `nps_score`: nota de satisfação do cliente em escala de 0 a 10.

Para leitura de negócio e modelagem classificatória, a nota também é convertida em categorias:

| Categoria | Regra |
|---|---|
| Detrator | NPS de 0 a 6 |
| Neutro | NPS 7 ou 8 |
| Promotor | NPS 9 ou 10 |

<a id="estrutura-do-repositorio"></a>
## 📁 Estrutura do Repositório

```text
.
|-- data/
|   `-- desafio_nps_fase_1.csv
|-- notebooks/
|   `-- tech_challenge_fase1.ipynb
|-- models/                        <- gerado ao executar o notebook completo
|   |-- nps_regressor.joblib
|   |-- nps_classifier.joblib
|   |-- model_metadata.json
|   `-- feature_schema.json
|-- reports/                       <- gerado ao executar o notebook completo
|   `-- <figuras exportadas>.png
|-- presentation/                  <- Slide de apresentação do case
|   `-- Apresentação_Tech_Challenge.pptx      
|-- requirements.txt
`-- README.md
```

<a id="entrega-executiva"></a>
## 🎥 Entrega Executiva
Este projeto também inclui materiais voltados para stakeholders e lideranças, focados em tomada de decisão:

* **[Slides de Apresentação](/presentation/Apresentação%20Tech%20Challenge.pptx):** Material visual com o contexto do problema, principais insights da EDA, fatores críticos de satisfação e recomendações práticas.

<a id="metodologia-e-desenvolvimento"></a>
## 🛠️ Metodologia e Desenvolvimento

O projeto seguiu a estrutura do framework **CRISP-DM** (Cross Industry Standard Process for Data Mining), que adota um padrão cíclico consolidado na indústria para desenvolver projetos de Data Science que agregam valor estratégico ao negócio. O projeto passou pelas seguintes etapas:

1. Entendimento do negócio;
2. Entendimento dos dados;
3. Preparação e auditoria da base;
4. Análise exploratória de dados;
5. Investigação de pontos de ruptura operacionais;
6. Avaliação estatística;
7. Modelagem preditiva;
8. Interpretação dos modelos;
9. Síntese executiva e recomendações de negócio.

Foram utilizadas duas abordagens complementares de modelagem:

| Abordagem | Objetivo |
|---|---|
| Regressão | Estimar a nota prevista de NPS em escala de 0 a 10 |
| Classificação | Estimar a categoria de NPS: Detrator, Neutro ou Promotor |

A regressão ajuda a estimar intensidade de satisfação, enquanto a classificação apoia a priorização operacional por categoria de risco.



<a id="principais-analises-realizadas"></a>
## 📊 Principais análises realizadas

O notebook contempla:

- distribuição do `nps_score` e das categorias Detrator, Neutro e Promotor;
- auditoria de qualidade dos dados;
- análise de assimetria, curtose e outliers;
- correlações de Pearson e Spearman;
- comparação operacional entre categorias de NPS;
- investigação de pontos de ruptura;
- avaliação de variáveis com risco de data leakage;
- treinamento e comparação de modelos de regressão;
- treinamento, calibração e avaliação de modelos de classificação;
- análise de resíduos;
- interpretação de importância de variáveis;
- explicabilidade com SHAP;
- geração de artefatos em `models/` e gráficos em `reports/`.


<a id="cuidados-contra-data-leakage"></a>
## ⚠ Cuidados contra data leakage

Foram excluídas da modelagem variáveis que poderiam comprometer a validade prática do modelo.

Colunas removidas:

| Coluna | Motivo |
|---|---|
| `customer_id` | Identificador único, sem poder preditivo generalizável |
| `order_id` | Identificador único, sem poder preditivo generalizável |
| `nps_score` | Variável alvo da regressão |
| `nps_category` | Target derivado para classificação |
| `csat_internal_score` | Indicador de satisfação coletado em contexto próximo ao NPS |
| `repeat_purchase_30d` | Informação de recompra posterior ao pedido, inadequada para alerta antecipado |

A variável `repeat_purchase_30d` foi mantida apenas na análise exploratória e no storytelling de negócio, pois ajuda a discutir a relação entre satisfação e comportamento de recompra. Ela não é utilizada como entrada nos modelos finais.


<a id="modelos-preditivos"></a>
## ⚙  Modelos preditivos

### Modelo de regressão

O modelo final de regressão salvo é um **Gradient Boosting Regressor** em pipeline scikit-learn, com tratamento de variáveis numéricas e categóricas.

Artefato salvo:

```text
models/nps_regressor.joblib
```

Métricas em holdout:

| MAE | RMSE | R² |
|---:|---:|---:|
| 1.20 | 1.50 | 0.643 |

O modelo de regressão estima a nota prevista de NPS em escala de 0 a 10.

## Modelo de classificação

O modelo final de classificação salvo é um **Random Forest Classifier calibrado**, utilizado para prever a categoria de NPS.

Artefato salvo:

```text
models/nps_classifier.joblib
```

Métricas em holdout:

| Accuracy | F1 macro | F1 weighted |
|---:|---:|---:|
| 0.856 | 0.796 | 0.843 |

Desempenho por classe:

| Classe | Precision | Recall | F1-score |
|---|---:|---:|---:|
| Detrator | 0.877 | 0.946 | 0.910 |
| Neutro | 0.655 | 0.422 | 0.514 |
| Promotor | 0.930 | 1.000 | 0.964 |

O classificador apresenta melhor desempenho para **Detrator** e **Promotor**, enquanto a classe **Neutro** permanece mais desafiadora por representar uma zona intermediária entre satisfação e insatisfação.

Do ponto de vista de negócio, o modelo é especialmente útil como ferramenta de alerta para clientes com risco de detratação.

<a id="como-reproduzir-o-projeto"></a>
## 🚀 Como Reproduzir o Projeto

### Passo 1: Clonar o Repositório
```bash
git clone https://github.com/seu-usuario/tech-challenge-nps.git
cd tech-challenge-nps
```

### Passo 2: Instalar Dependências
```bash
pip install -r requirements.txt
```

### Passo 3: Executar a Análise
```bash
jupyter notebook notebooks/Tech-Challenge-Fase-1.ipynb
```

Execute todas as células do início ao fim.

Ao final da execução, serão gerados:

- modelos treinados em `models/`;
- metadata do modelo;
- schema das features;
- figuras exportadas em `reports/`.

<a id="como-usar-os-modelos-treinados"></a>
## 🔖 Como usar os modelos treinados

### Usar o modelo de regressão

```python
import joblib
import pandas as pd

regressor = joblib.load("models/nps_regressor.joblib")

novos_dados = pd.read_csv("data/novos_pedidos.csv")

novos_dados["nps_previsto"] = regressor.predict(novos_dados)
```

### Usar o modelo de classificação

```python
import joblib
import pandas as pd

classifier = joblib.load("models/nps_classifier.joblib")

novos_dados = pd.read_csv("data/novos_pedidos.csv")

novos_dados["categoria_nps_prevista"] = classifier.predict(novos_dados)
```

Caso o classificador esteja calibrado, também é possível extrair probabilidades por classe:

```python
probabilidades = classifier.predict_proba(novos_dados)
classes = classifier.classes_

probabilidades_df = pd.DataFrame(probabilidades, columns=classes)
```


<a id="principais-insights-de-negocio"></a>
## 📋 Principais insights de negócio

- A base apresenta forte concentração de **Detratores**, com 84,0% dos registros.
- O NPS agregado da base é **-66,0**, indicando uma experiência geral negativa.
- O principal fator operacional associado à queda do NPS é o **atraso na entrega**.
- O ponto de ruptura mais relevante ocorre já a partir de **1 dia de atraso**.
- **Reclamações**, **contatos com atendimento** e **tempo de resolução** também aparecem como sinais importantes de fricção.
- Variáveis demográficas e regionais apresentam menor impacto individual, sugerindo que a insatisfação está mais associada à operação do que ao perfil do cliente.
- A análise SHAP confirma que os modelos são explicados principalmente por variáveis operacionais acionáveis.

<a id="recomendacoes-de-negocio"></a>
## ✅ Recomendações de negócio

Com base nos resultados, recomenda-se:

- priorizar pedidos com atraso na entrega;
- criar alertas para clientes com múltiplas reclamações;
- acelerar o tempo de resolução de problemas;
- monitorar clientes com múltiplos contatos com atendimento;
- usar o score previsto como apoio à priorização em filas de CX;
- combinar o modelo com regras operacionais simples para ações preventivas;
- acompanhar métricas por safra para identificar drift e perda de performance ao longo do tempo.

<a id="limitacoes"></a>
## ❗ Limitações

Este projeto possui algumas limitações importantes:

- a base é fictícia e deve ser validada contra dados reais antes de uso produtivo;
- o modelo identifica associações, não causalidade;
- a classe Neutro apresenta maior ambiguidade e menor desempenho preditivo;
- variáveis operacionais só devem ser usadas se estiverem disponíveis antes da pesquisa NPS;
- o modelo deve ser monitorado periodicamente para identificar drift;
- decisões sensíveis não devem ser tomadas exclusivamente com base na predição do modelo.

<a id="proximos-passos"></a>
## 💡 Próximos passos

Possíveis evoluções do projeto:

- testar uma abordagem binária para risco de detrator;
- incluir custo de intervenção e valor do cliente para priorização econômica;
- testar técnicas adicionais de balanceamento de classes;
- monitorar drift por safra, região e canal;
- integrar o score previsto a uma régua real de CX;
- criar dashboards executivos para acompanhamento contínuo dos principais drivers de NPS.

<a id="resumo-executivo"></a>
## 💼 Resumo executivo

O projeto demonstra que é possível antecipar risco de insatisfação utilizando sinais operacionais da jornada de compra.

A principal conclusão é que o NPS não é explicado prioritariamente por perfil demográfico ou região, mas por fatores acionáveis da operação, especialmente:

- atraso na entrega;
- reclamações;
- contatos com atendimento;
- tempo de resolução.

Assim, a solução proposta não deve ser interpretada apenas como um modelo estatístico, mas como um mecanismo de priorização operacional para apoiar ações preventivas de CX, logística e atendimento.
