# 🧬 trabalho-TEsClassification
Trabalho realizado para a disciplina **SCC02713 - Introdução à Bioinformática** do **Instituto de Ciências Matemáticas e de Computação (ICMC-USP)**.

## 🎯 Objetivo
Este projeto tem como objetivo construir um **modelo de classificação de Elementos Transponíveis (TEs)** da planta *Zea mays*, utilizando dados do **Atlas dos Elementos Transponíveis em Plantas** e o **genoma de referência do NCBI**.

O fluxo completo inclui:
1. Montagem do conjunto de dados (extração das sequências genômicas dos TEs)
2. Extração de atributos com *MathFeature* ou *Pse-in-One*
3. Treinamento e avaliação dos classificadores com *scikit-learn*
4. Elaboração de relatório e vídeo de divulgação

---
## 📊 Resultados Experimentais

Para avaliar o desempenho da classificação, testamos o modelo **XGBoost** sob três estratégias diferentes de tratamento de desbalanceamento de classes: **Sample Weight**, **SMOTE** e **None** (Sem tratamento).

Abaixo estão os resultados comparativos:

### 1. Resumo Comparativo

| Estratégia | Acurácia Global | Weighted F1-Score | Observação Principal |
|:----------:|:---------------:|:-----------------:|:---------------------|
| **None** | **58.91%** | **0.55** | Alta acurácia, mas ignora classes minoritárias. |
| **SMOTE** | 36.58%          | 0.41              | Melhor equilíbrio entre classes, mas gera muitos falsos positivos. |
| **Weights**| 35.88%          | 0.41              | Resultado similar ao SMOTE, com ligeira queda na performance. |

---

### 2. Detalhamento por Estratégia

#### A. Estratégia: NONE (Treinamento Padrão)
*Nesta abordagem, o modelo foi treinado com os dados originais, preservando o desbalanceamento natural (dominância de LTR).*

> **Acurácia:** 0.5891

| Classe | Precision | Recall | F1-Score | Suporte |
|:------:|:---------:|:------:|:--------:|:-------:|
| Helitron | **0.92** | 0.00 | 0.00 | 7.209 |
| LINE | 0.65 | 0.01 | 0.01 | 3.238 |
| **LTR** | 0.78 | 0.69 | **0.73** | 56.176 |
| MITE | 0.11 | 0.00 | 0.00 | 7.730 |
| SINE | 0.74 | 0.06 | 0.10 | 1.070 |
| TIR | 0.40 | **0.81** | 0.54 | 24.308 |

#### B. Estratégia: SMOTE (Synthetic Minority Over-sampling Technique)
*Foi aplicada a geração de dados sintéticos para aumentar a representatividade das classes minoritárias.*

> **Acurácia:** 0.3658

| Classe | Precision | Recall | F1-Score | Suporte |
|:------:|:---------:|:------:|:--------:|:-------:|
| Helitron | 0.16 | 0.39 | 0.22 | 7.209 |
| LINE | 0.06 | 0.16 | 0.08 | 3.238 |
| **LTR** | **0.80** | 0.34 | 0.48 | 56.176 |
| MITE | 0.14 | 0.35 | 0.20 | 7.730 |
| SINE | 0.06 | 0.22 | 0.10 | 1.070 |
| TIR | 0.44 | 0.45 | 0.44 | 24.308 |

#### C. Estratégia: SAMPLE_WEIGHT (Ponderação de Classes)
*O modelo atribuiu pesos maiores aos erros cometidos nas classes minoritárias durante o treinamento.*

> **Acurácia:** 0.3588

| Classe | Precision | Recall | F1-Score | Suporte |
|:------:|:---------:|:------:|:--------:|:-------:|
| Helitron | 0.16 | 0.39 | 0.23 | 7.209 |
| LINE | 0.05 | 0.19 | 0.08 | 3.238 |
| **LTR** | 0.79 | 0.36 | 0.49 | 56.176 |
| MITE | 0.16 | 0.47 | 0.24 | 7.730 |
| SINE | 0.07 | 0.20 | 0.10 | 1.070 |
| TIR | 0.42 | 0.34 | 0.38 | 24.308 |

---

## Como Começar (Instruções de Execução)
Este repositório usa `.gitignore` para ignorar arquivos de dados grandes e processados. Para clonar o projeto e recriar os arquivos necessários, siga estas etapas:

### 1. Clone e Configure o Ambiente
```bash
# 1. Clone o repositório
git clone [https://github.com/LuizCorrei4/trabalho-TEsClassification.git](https://github.com/LuizCorrei4/trabalho-TEsClassification.git)
cd trabalho-TEsClassification

# 2. Crie um ambiente virtual (recomendado)
python -m venv venv
source venv/bin/activate  # No Windows: venv\Scripts\activate

# 3. Instale as dependências
pip install -r requirements.txt
```
### 2. Execute os Notebooks na Ordem

Você **deve** executar os notebooks na ordem correta, pois eles dependem dos arquivos gerados pelo notebook anterior.

---

#### 1. `01_dataset_construction.ipynb`

- **O que faz:**  
  Baixa os genomas FASTA do NCBI e constrói o dataset bruto (`TE_dataset_final.csv`).

- **Ação:**  
  Execute todas as células.

---

#### 2. `02_eda_dataset_final.ipynb`

- **O que faz:**  
  Realiza a análise exploratória e limpa erros básicos (como 'N'), gerando o arquivo  
  `TE_dataset_final_clean.csv`.

- **Ação:**  
  Execute todas as células.

---

#### 3. `03_pre_processing.ipynb`

- **O que faz:**  
  Aplica o pré-processamento definido na EDA (remove sequências < 50bp, aplica log-transform no comprimento) e salva  
  `TE_dataset_final_pre_processed.csv`.

- **Ação:**  
  Execute todas as células.

---

#### 4. `04_dataset_balancing.ipynb`

- **O que faz:**  
  Carrega o dataset pré-processado, divide-o em treino/teste e aplica o balanceamento conservador.

- **Ação:**  
  Execute todas as células. Isso criará a pasta `data/train_test_split/`.

---

### 3. Próxima Etapa

Após executar os 4 notebooks, você estará pronto para a **Extração de Atributos**, que será feita no notebook  
`05_feature_extraction.ipynb`.


## Etapas do Trabalho

### 1. Coleta de Dados (`01_data_set_construction.ipynb`)
- Baixar os 6 arquivos `.gff3` do [Atlas dos Elementos Transponíveis](http://apte.cp.utfpr.edu.br/download)
- Filtrar apenas as linhas com `Strand = '+'`
- Extrair as colunas `Chr` (cromossomo), `Start`, `End` e a classe correspondente
- Resultado: um conjunto de dados com as localizações dos elementos transponíveis

### 2. Extração de Sequências (`01_data_set_construction.ipynb`)
- Baixar os cromossomos do *Zea mays* no [NCBI Datasets](https://www.ncbi.nlm.nih.gov/datasets/)
- Usar **BioPython** para recuperar as sequências correspondentes
- Gerar `TE_dataset_final.csv` com as colunas:
  - Cromossomo | Sequência de TE | Classe

---

### 3. Análise Exploratória (`02_eda_dataset_final.ipynb`)
- Analisou o dataset `TE_dataset_final.csv` com foco em:
  - Estatísticas básicas e integridade dos dados
  - Distribuição das classes e cromossomos
  - Comprimento das sequências
  - Composição nucleotídica (A, T, C, G)
  - Correlações entre variáveis
- Principais achados:
  - Desbalanceamento extremo entre classes (LTR = 56%, SINE = 1%)
  - Sequências muito curtas (<50 bp) e muito longas (>10.000 bp)
  - Pouca variação de composição nucleotídica entre classes (~53% AT)
  - Correlação moderada entre **classe** e **comprimento** (-0.33)
- Ações recomendadas:
  - Remover sequências inválidas e com “N”
  - Aplicar transformação logarítmica ao comprimento
  - Adotar AUC-PR como métrica principal para ML
  - Focar no balanceamento entre classes
- Gera: `TE_dataset_final_clean.csv`

---

### 4. Pré-processamento (`03_pre_processing.ipynb`)
- Carrega o dataset limpo `TE_dataset_final_clean.csv`
- Remove as sequências muito curtas (<50 bp)
- Aplica **transformação logarítmica** ao comprimento para reduzir assimetria
- Realiza etapas básicas de limpeza e engenharia de features
- Salva o dataset processado como `TE_dataset_final_pre_processed.csv`

---

### 5. Balanceamento (`04_dataset_balancing.ipynb`)
- Divide o dataset em **treino (70%)** e **teste (30%)**
- Aplica **balanceamento conservador** apenas no conjunto de treino:
  - **Oversampling** por duplicação para classes raras (SINE, LINE)
  - **Undersampling** para classe majoritária (LTR)
- Evita técnicas como SMOTE para não criar sequências biologicamente artificiais
- Gera os arquivos:
  - `data/train_test_split/train.csv`
  - `data/train_test_split/test.csv`

---

### 6. Extração de Atributos (`05_feature_extraction.ipynb`)
- Utilizar **MathFeature** ou **Pse-in-One** para converter as sequências em vetores numéricos
- Descritores recomendados:
  - k-mers (2–4 nucleotídeos)
  - Entropia
  - Autocorrelação
- Gerar `Features.csv`, cada sequência será então um vetor com colunas que contem um valor das características:
  - f1 (feature 1), f2 (feature 2), f3, ..., Class

---

### 7. Treinamento e Avaliação (`06_training_model.ipynb`)
- Treinar classificadores com **scikit-learn** (Random Forest, SVM, etc.)
- Avaliar com a **Área sob a Curva Precisão–Revocação (AUC-PR)**
- Realizar **validação cruzada estratificada** para evitar viés de classe

---


## 📂 Estrutura do Repositório (após rodar os notebooks)

```bash
📁 trabalho-TEsClassification/
│
├── data/                             # → Dados brutos, filtrados e datasets
│   ├── arquivos_TEAnnotation_brutos/   #   → Arquivos GFF3 brutos
│   ├── arquivos_TEAnnotation_filtrados/  #   → Arquivos GFF3 filtrados
│   ├── fasta_genomas/                #   → Genomas em formato FASTA
│   ├── train_test_split/                #   → Arquivos de teste e treino separados
│   ├── TE_dataset_final.csv          #   → Dataset gerado
│   └── TE_dataset_final_clean.csv    #   → Dataset limpo
│   └── TE_dataset_final_pre_processed.csv    #   → Dataset limpo e pré-processado 
│
├── features/                         # → Vetores de atributos extraídos (a ser preenchido)
│
├── notebooks/                        # → Notebooks Jupyter
│   ├── 01_dataset_construction.ipynb #   → Script de construção do dataset
│   └── 02_eda_dataset_final.ipynb    #   → Análise exploratória dos dados (+ limpeza de sequências problemáticas)
|   └── 03_pre_processing.ipynb        #   → Pré-processamento dos dados
|   └── 04_dataset_balancing.ipynb     #   → Balanceamento do dataset
|   └── 05_feature_extraction.ipynb    #   → Extração de atributos
|   └── 06_training_model.ipynb        #   → Treinamento e avaliação do modelo
│
├── results/                          # → Gráficos da análise exploratória
│   ├── analise_comprimento_das_sequencias.png
│   ├── composicao_nucleotideos_por_classe.png
│   └── matriz_de_correlacao.png
│                    # → Roteiro, slides e link do vídeo (a ser preenchido)
│
├── .gitattributes
├── .gitignore                        # → Arquivos ignorados pelo Git
├── README.md                         # → Este arquivo
└── requirements.txt                  # → Dependências do projeto
```

---

## ⚙️ Ferramentas Utilizadas
- **BioPython**
- **pandas**
- **scikit-learn**
- **MathFeature** / **Pse-in-One**
- **matplotlib**, **numpy**, **seaborn**
- **Overleaf** (para o relatório)

---

## 👥 Integrantes
| Nome | Nº USP | 
|------|--------|
| [Luiz Gabriel Correia dos Santos] | [15639682] |
| [Victor Silva Botelho] | [15645421] |
| [João Pedro Barbosa Madeira] | [13683038] |
---

## 🔗 Links Úteis
- 🧬 [Atlas dos Elementos Transponíveis (APTE)](http://apte.cp.utfpr.edu.br/download)  
- 🧫 [NCBI Datasets - Zea mays](https://www.ncbi.nlm.nih.gov/datasets/)  
- 🧠 [MathFeature - Extração de Atributos](https://github.com/Bonidia/MathFeature)  
- 🧩 [Pse-in-One 2.0](https://www.scirp.org/journal/paperinformation?paperid=75771)  
- 📊 [Scikit-learn - Biblioteca de ML](https://scikit-learn.org/stable/)  
- 🧾 [Template SBC (Overleaf)](https://www.overleaf.com/latex/templates/sbc-conferences-template/blbxwjwzdngr)  

---

## 📄 Licença
Projeto desenvolvido exclusivamente para fins acadêmicos na disciplina **SCC02713 - Introdução à Bioinformática (ICMC-USP)**.
