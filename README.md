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
## 2. Execute os Notebooks na Ordem

Você **deve** executar os notebooks na ordem correta, pois eles dependem dos arquivos gerados pelo notebook anterior.

---

### 1. `01_dataset_construction.ipynb`

- **O que faz:**  
  Baixa os genomas FASTA do NCBI e constrói o dataset bruto (`TE_dataset_final.csv`).

- **Ação:**  
  Execute todas as células.

---

### 2. `02_eda_dataset_final.ipynb`

- **O que faz:**  
  Realiza a análise exploratória e limpa erros básicos (como 'N'), gerando o arquivo  
  `TE_dataset_final_clean.csv`.

- **Ação:**  
  Execute todas as células.

---

### 3. `03_pre_processing.ipynb`

- **O que faz:**  
  Aplica o pré-processamento definido na EDA (remove sequências < 50bp, aplica log-transform no comprimento) e salva  
  `TE_dataset_final_pre_processed.csv`.

- **Ação:**  
  Execute todas as células.

---

### 4. `04_dataset_balancing.ipynb`

- **O que faz:**  
  Carrega o dataset pré-processado, divide-o em treino/teste e aplica o balanceamento conservador.

- **Ação:**  
  Execute todas as células. Isso criará a pasta `data/train_test_split/`.

---

## 3. Próxima Etapa

Após executar os 4 notebooks, você estará pronto para a **Etapa 3 (Extração de Atributos)**, que será feita no notebook  
`05_feature_extraction.ipynb`.


## 🧩 Etapas do Trabalho

### 1. Coleta de Dados (feito em 01_data_set_construction.ipynb)
- Baixar os 6 arquivos `.gff3` do [Atlas dos Elementos Transponíveis](http://apte.cp.utfpr.edu.br/download)
- Filtrar apenas as linhas com `Strand = '+'`
- Extrair as colunas `Chr` (cromossomo), `Start`, `End` e a classe correspondente
- Resultado: um conjunto de dados com as localizações dos elementos transponíveis

### 2. Extração de Sequências (feito em 01_data_set_construction.ipynb)
- Baixar os cromossomos do *Zea mays* no [NCBI Datasets](https://www.ncbi.nlm.nih.gov/datasets/)
- Usar **BioPython** para recuperar as sequências correspondentes
- Gerar `TE_dataset_final.csv` com as colunas:
  - Chromosome | Sequence | Class

### 3. Extração de Atributos
- Utilizar **MathFeature** ou **Pse-in-One** para converter as sequências em vetores numéricos
- Escolher um ou mais descritores (ex.: k-mers, entropia, autocorrelação)
- Gerar `Features.csv` com colunas:
  - f1, f2, f3, ..., Class
 

### 4. Treinamento e Avaliação
- Dividir os dados em **70% treino** e **30% teste**
- Aplicar **normalização** ou **padronização**
- Treinar classificadores com **scikit-learn** (Random Forest, SVM, etc.)
- Avaliar usando a **Área sob a Curva Precisão–Revocação (AUC-PR)**

---

## 📂 Estrutura do Repositório

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
│
├── results/                          # → Gráficos da análise exploratória
│   ├── analise_comprimento_das_sequencias.png
│   ├── composicao_nucleotideos_por_classe.png
│   └── matriz_de_correlacao.png
│
│
├── video/                            # → Roteiro, slides e link do vídeo (a ser preenchido)
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
