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

## 🧩 Etapas do Trabalho

### 1. Coleta de Dados
- Baixar os 6 arquivos `.gff3` do [Atlas dos Elementos Transponíveis](http://apte.cp.utfpr.edu.br/download)
- Filtrar apenas as linhas com `Strand = '+'`
- Extrair as colunas `Chr`, `Start`, `End` e a classe correspondente

### 2. Extração de Sequências
- Baixar os cromossomos do *Zea mays* no [NCBI Datasets](https://www.ncbi.nlm.nih.gov/datasets/)
- Usar **BioPython** para recuperar as sequências correspondentes
- Gerar `Dataset_Final.csv` com as colunas:
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

## 🗂️ Estrutura do Repositório

📁 trabalho-TEsClassification/

│

├── data/ → arquivos .gff3, fasta e dataset final

├── features/ → vetores de atributos extraídos

├── notebooks/ → notebooks do Google Colab

├── results/ → gráficos, métricas e modelos

├── report/ → artigo científico e figuras

├── video/ → roteiro, slides e link do vídeo

└── README.md


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
