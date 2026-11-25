# AGENTS.md — Instruções para o Projeto ICD (Predicting Cardiac Diseases in Children)

## Contexto e Objetivo
Este repositório contém o projeto prático de **Introdução à Ciência de Dados (ICD)** (Mestrado em Inteligência Artificial, FCUP/FEUP).
- **Entregável principal:** `notebooks/projeto_icd_cardiopatias.ipynb` (funciona simultaneamente como código executável e relatório final).
- **Idioma:** Todo o texto explicativo em Markdown, comentários de código e títulos de gráficos devem ser escritos em **Português (Portugal)**.
- **Objetivo técnico:** Limpar e transformar o dataset clínico pediátrico (`data/raw/UCMF(5).xls`), realizar análise exploratória (univariada, bivariada e multivariada), aplicar métodos de *feature importance* para identificar os principais preditores de patologias cardíacas (`NORMAL X ANORMAL`) e treinar/comparar modelos de aprendizagem automática.

## Ambiente e Caminhos
- **Ambiente Virtual:** Usar sempre `./venv/bin/python` (nunca `.venv` nem Python global).
- **Dataset bruto:** `data/raw/UCMF(5).xls` (folha `UCMF_CORRIGIDO`, 17 873 registos, 21 colunas — requer `xlrd`). Nunca alterar este ficheiro.
- **Dataset limpo:** Exportar o resultado da Secção 2 para `data/processed/ucmf_cleaned.csv`.
- **Documentação de referência em `docs/`:**
  - `docs/t1-V1.pdf`: Enunciado e estrutura obrigatória do relatório.
  - `docs/DataAnalysis_GoodPractices.pdf`: Regras metodológicas de pré-processamento e análise.
  - `docs/imc_sandra.pdf`: Curvas de crescimento e percentis de IMC da DGS (0–24 meses e 2–20 anos).
  - `docs/blood_pressure_children.pdf`: Tabelas pediátricas de PAS/PAD por idade e percentil de altura.
  - `docs/fluxoConsultaCardiologica.pdf`: Fluxograma clínico de diagnóstico cardiológico pediátrico.

## Estrutura Obrigatória do Notebook (`notebooks/projeto_icd_cardiopatias.ipynb`)
Qualquer edição ao notebook deve respeitar estritamente esta sequência e intercalar células `Markdown` bem fundamentadas antes e depois de cada bloco de código:

1. **Secção 1 — Dados em Bruto (*Raw Data*):**
   - Classificar todas as 21 variáveis por escala estatística (*nominal*, *ordinal*, *binary*, *interval-scaled*, *ratio-scaled*).
   - Mostrar sumários estatísticos, contagem de omissos, duplicados e visualizações iniciais (histogramas/boxplots) evidenciando anomalias.
   - Listar explicitamente todas as transformações necessárias.
2. **Secção 2 — Pré-processamento (*Preprocessed Data*):**
   - Remover `ID` (identificador) e `HDA2` (>96% de valores omissos).
   - Remover registos duplicados (ignorando `ID`) e linhas sem variável alvo (`NORMAL X ANORMAL` nulo).
   - Uniformizar categorias inconsistentes (`SEXO`, `SOPRO`, `PULSOS`, `B2`, `NORMAL X ANORMAL`).
   - Converter `IDADE` e `FC` para numérico; remover/corrigir valores fisiologicamente impossíveis (`Peso <= 0`, `Altura <= 0`, `IDADE < 0` ou `Atendimento < DN`, tensões arteriais absurdas).
   - Recalcular `IMC` ($\text{Peso} / \text{Altura (m)}^2$) onde estiver corrompido ou em falta.
   - Criar intervalos clínicos pediátricos (faixas etárias e categorização de IMC/PA) com base nos PDFs clínicos.
   - Guardar o dataset limpo em `data/processed/ucmf_cleaned.csv`.
3. **Secção 3 — Descrição Básica Pós-Limpeza (*Basic Description*):**
   - Repetir sumários, medidas de dispersão, histogramas, boxplots e curvas de densidade após limpeza.
4. **Secção 4 — Análise e Modelação (*Analysis*):**
   - **Análise Bivariada:** Correlações (Pearson/Spearman) e associações com `NORMAL X ANORMAL`.
   - **Análise Multivariada & Feature Importance:** Mutual Information, clustering para dados mistos (ex.: distância de Gower ou K-Prototypes) e ranking de atributos via Filtro, *Wrapper* e *Embedded*.
   - **Modelos Preditivos:** Treinar e avaliar **Decision Trees**, **Support Vector Machines (SVM)**, **Bayesian Networks** (ou Naive Bayes) e **Random Forest** usando validação cruzada estratificada e métricas adequadas a classes desbalanceadas (*Recall/Sensibilidade*, *Precision*, *F1-Score*, *ROC-AUC*).
5. **Secção 5 — Discussão e Conclusões Principais (*Discussion and Main Conclusions*):**
   - Comparar o ranking de atributos obtido com o fluxograma médico (`docs/fluxoConsultaCardiologica.pdf`) e justificar a escolha do melhor modelo clínico.

## Regras de Código e Git
- Evitar data leakage: aplicar `StandardScaler` / codificação (*One-Hot* / *Ordinal*) dentro de `sklearn.pipeline.Pipeline` apenas nos conjuntos de treino.
- Manter os gráficos limpos, legíveis, com títulos, eixos identificados e legendas em Português.
- Nunca fazer commit da pasta `venv/` ou de ficheiros temporários.