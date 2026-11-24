# Predicting Cardiac Diseases in Children — ICD

Projeto prático desenvolvido no âmbito da unidade curricular de **Introdução à Ciência de Dados (ICD)** — Mestrado em Inteligência Artificial (FCUP/FEUP, Universidade do Porto).

**Data de Apresentação:** 16 de dezembro de 2026

---

## 🎯 Objetivo

O objetivo principal deste trabalho é aplicar técnicas de análise exploratória, pré-processamento orientado ao domínio clínico e métodos de *feature importance* para identificar os atributos mais preditivos de patologias cardíacas em crianças (`NORMAL X ANORMAL`), bem como treinar e comparar modelos de aprendizagem automática supervisionada.

O dataset original (`UCMF(5).xls`) contém **17 873 registos clínicos** anonimizados de pacientes entre os 0 e os 19 anos, recolhidos no Real Hospital Português (Brasil).

---

## 📁 Estrutura do Repositório

    projeto_icd/
    ├── data/
    │   ├── raw/
    │   │   └── UCMF(5).xls                      # Dataset original intacto
    │   └── processed/                           # Dados limpos e transformados exportados pelo notebook
    ├── docs/
    │   ├── t1-V1.pdf                            # Enunciado e requisitos do relatório
    │   ├── DataAnalysis_GoodPractices.pdf       # Guia metodológico de análise de dados
    │   ├── imc_sandra.pdf                       # Circular Normativa da DGS (Curvas de crescimento e IMC)
    │   ├── blood_pressure_children.pdf          # Tabelas pediátricas de tensão arterial (PAS/PAD)
    │   ├── fluxoConsultaCardiologica.pdf        # Fluxograma médico de diagnóstico cardiológico
    │   └── Então vamos começar - Felipe Mourato.pdf # Guia prático de interpretação de percentis clínicos
    ├── notebooks/
    │   └── projeto_icd_cardiopatias.ipynb       # Notebook principal (Relatório + Código executável)
    ├── .gitignore                               # Exclusão do venv e ficheiros temporários
    ├── requirements.txt                         # Dependências Python do projeto
    └── README.md                                # Documentação do repositório

---

## ⚙️ Configuração e Execução

Para reproduzir os resultados localmente (Linux/macOS):

1. **Clonar o repositório:**

       git clone <URL_DO_TEU_REPOSITORIO>
       cd projeto_icd

2. **Criar e ativar o ambiente virtual (`venv`):**

       python3 -m venv venv
       source venv/bin/activate

3. **Instalar as dependências:**

       pip install -r requirements.txt

4. **Abrir e executar o notebook:**
   Abrir `notebooks/projeto_icd_cardiopatias.ipynb` no VS Code (selecionando o kernel `venv`) ou iniciar via terminal:

       jupyter notebook notebooks/projeto_icd_cardiopatias.ipynb

---

## 📊 Estrutura do Relatório (Notebook)

O notebook está organizado sequencialmente de acordo com as diretrizes do enunciado (`docs/t1-V1.pdf`)[cite: 28, 29]:

1. **Dados em Bruto (*Raw Data*):** Classificação estatística das 21 variáveis, análise exploratória inicial (sumários, histogramas, boxplots) e levantamento de inconsistências (duplicados, valores omissos, erros `#VALUE!`, registos fisiologicamente impossíveis)[cite: 28].
2. **Pré-processamento (*Preprocessed Data*):** Remoção de atributos irrelevantes/omissos (`ID`, `HDA2`), tratamento de duplicados, normalização de categorias, imputação/filtragem de outliers e engenharia de atributos clínicos (faixas etárias pediátricas e percentis de IMC/tensão arterial)[cite: 1, 27, 28].
3. **Descrição Básica Pós-Limpeza:** Comparação estatística e visual das distribuições após o tratamento dos dados[cite: 28, 29].
4. **Análise e Modelação:**
   * **Análise Bivariada e Multivariada:** Correlações, Informação Mútua (*Mutual Information*) e *Clustering* para identificação de perfis clínicos[cite: 2, 27, 29].
   * **Feature Selection / Importance:** Ranking de atributos por métodos de Filtro, *Wrapper* e *Embedded*[cite: 2, 27].
   * **Modelos Preditivos:** Treino, validação cruzada e comparação de *Decision Trees*, *Support Vector Machines (SVM)*, *Bayesian Networks* e *Random Forest*[cite: 28, 29].
5. **Discussão e Conclusões:** Interpretação clínica das variáveis mais relevantes face ao fluxograma cardiológico e análise comparativa de desempenho[cite: 26, 29].