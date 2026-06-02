# 📊 Análise Estatística — Desempenho de Alunos em Exames

> **Entrega da Tarefa — Semana 4 | Asimov Jr**  
> Aplicação prática dos conteúdos de Estatística I & II sobre o dataset *Students Performance in Exams*

---

## 📌 Sobre o Projeto

Este projeto foi desenvolvido como entrega da **tarefa da semana 4 da Asimov Jr**, com o objetivo de aplicar de forma integrada os conceitos estudados nas disciplinas de **Estatística I e II**.

A análise é conduzida inteiramente em Python, dentro de um Jupyter Notebook estruturado em 11 capítulos, cobrindo desde a exploração inicial dos dados até testes de hipótese, modelagem probabilística e métricas de erro. O dataset utilizado é o [Students Performance in Exams](https://www.kaggle.com/datasets/spscientist/students-performance-in-exams), disponível publicamente no Kaggle, contendo informações sobre o desempenho de 1.000 alunos em matemática, leitura e escrita, junto a variáveis socioeconômicas e demográficas.

---

## 🗂️ Estrutura do Notebook

O notebook está organizado em 11 seções sequenciais:

| # | Capítulo | Conteúdo Principal |
|---|---|---|
| 1 | Importação e Exploração Inicial | Carregamento, tradução das colunas, tipos de dados, valores ausentes |
| 2 | Análise Exploratória (EDA) e Amostragem | Distribuições categóricas, amostragem aleatória simples |
| 3 | Medidas de Centralidade e Dispersão | Média, mediana, moda, desvio padrão, CV, assimetria, curtose, IQR |
| 4 | Probabilidade e Distribuição Normal | Shapiro-Wilk, QQ-plots, histogramas, cálculo de probabilidades |
| 5 | Visualizações Gráficas | Barras, scatterplots, heatmap de correlação, violinplots |
| 6 | Intervalos de Confiança | IC para médias (t de Student) e para proporções (Wilson) |
| 7 | Testes de Hipótese | Teste t unilateral, bilateral por gênero e por curso preparatório |
| 8 | Distribuições t, Binomial e Poisson | Aplicações práticas das três distribuições |
| 9 | Testes de Comparação | Qui-Quadrado (×2), ANOVA de um fator |
| 10 | Métricas de Erro e Significância | Regressão linear, EAM, EQM, REQM, R², d de Cohen |
| 11 | Conclusões Finais | Principais achados e recomendações pedagógicas |

---

## 🛠️ Ferramentas e Bibliotecas

### Ambiente
- **Python 3.11+**
- **Jupyter Notebook**

### Bibliotecas utilizadas

#### `pandas`
Responsável por toda a manipulação tabular dos dados: carregamento do CSV, renomeação de colunas, tradução de valores categóricos, agrupamentos com `groupby`, criação de tabelas de contingência com `crosstab` e cálculo de estatísticas descritivas com `describe`.

#### `numpy`
Utilizado para operações matemáticas vetorizadas: cálculo de raízes quadradas, criação de arrays contínuos para plotar curvas de distribuição (`np.linspace`), e operações de álgebra usadas nas métricas de erro (EQM, REQM).

#### `matplotlib`
Biblioteca base para todos os gráficos do projeto. Responsável por histogramas, gráficos de barras, scatterplots, gráficos de resíduos, curvas de distribuições de probabilidade e o gráfico de intervalos de confiança com barras de erro.

#### `seaborn`
Camada de alto nível sobre o matplotlib, utilizada nos gráficos estatísticos: `countplot` (distribuições categóricas), `boxplot` (ANOVA), `violinplot` (comparação por curso preparatório) e `heatmap` (correlação entre disciplinas).

#### `scipy.stats`
Núcleo da análise inferencial do projeto. Funções utilizadas:

| Função | Aplicação no projeto |
|---|---|
| `shapiro` | Teste de normalidade de Shapiro-Wilk |
| `norm` | Cálculo de probabilidades via distribuição normal e histogramas teóricos |
| `t` (t_dist) | Valor crítico para intervalos de confiança e distribuição t de Student |
| `binom` | PMF e CDF da distribuição binomial |
| `poisson` | PMF da distribuição de Poisson |
| `ttest_1samp` | Teste t de uma amostra (unilateral) |
| `ttest_ind` | Teste t de duas amostras independentes (bilateral) |
| `levene` | Teste de igualdade de variâncias (homocedasticidade) |
| `chi2_contingency` | Teste Qui-Quadrado de independência |
| `f_oneway` | ANOVA de um fator |
| `linregress` | Regressão linear simples |
| `probplot` | Geração dos QQ-plots |

#### `statsmodels`
Utilizado exclusivamente para o cálculo do **intervalo de confiança para proporções pelo método de Wilson** (`proportion_confint`), que é mais preciso que o método clássico quando a proporção está próxima dos extremos 0 ou 1.

#### `warnings`
Importado apenas para suprimir alertas de terceiros durante a execução do notebook, mantendo o output limpo. Não tem papel analítico.

---

## 📈 Análise Estatística — Visão Geral

### Estatística Descritiva
Para cada uma das três disciplinas (matemática, leitura e escrita), foram calculadas: média, mediana, moda, desvio padrão, variância, coeficiente de variação, assimetria, curtose, quartis (Q1 e Q3), amplitude interquartil (IQR), mínimo e máximo.

### Normalidade
A aderência à distribuição normal foi verificada de duas formas complementares: o **teste de Shapiro-Wilk** (formal, com p-valor) e os **QQ-plots** (visual). Com n=1.000, o teste formal tende a rejeitar a normalidade perfeita mesmo com pequenos desvios; os QQ-plots confirmaram aderência satisfatória nas regiões centrais das distribuições.

### Probabilidades
Usando os parâmetros empíricos (μ e σ) de matemática como estimativas da distribuição normal, foram calculadas probabilidades de eventos práticos, como a chance de um aluno aleatório tirar nota acima de 70 ou ficar abaixo de 50.

### Intervalos de Confiança
Foram construídos intervalos com 95% de confiança para as **médias** de cada disciplina (usando a distribuição t de Student) e para as **proporções de aprovação** (nota ≥ 60, usando o método de Wilson). Com n=1.000, os intervalos para médias têm amplitude inferior a 3 pontos, demonstrando alta precisão nas estimativas.

### Testes de Hipótese
Três testes t foram realizados com formulações distintas:
- **Unilateral (H1: μ > 65):** verificou se a média de matemática supera o valor de referência 65.
- **Bilateral por gênero:** comparou as médias de matemática entre homens e mulheres, precedido do teste de Levene para homocedasticidade.
- **Bilateral por curso preparatório:** avaliou o impacto do curso sobre o desempenho, com resultado altamente significativo (p << 0,001).

### Distribuições de Probabilidade
Cada distribuição foi aplicada a um cenário real do dataset:
- **t de Student:** construção de IC com sub-amostra pequena (n=25), ilustrando o efeito das caudas pesadas.
- **Binomial:** probabilidade de exatamente k alunos obterem nota ≥ 70 em leitura, em grupos de 20.
- **Poisson:** modelagem da frequência esperada de notas muito baixas (< 40) por turma de 30 alunos.

### Testes de Comparação
- **Qui-Quadrado (gênero × curso preparatório):** ausência de associação — gênero não influencia a participação no curso.
- **Qui-Quadrado (almoço × aprovação):** associação significativa — renda familiar impacta a taxa de aprovação em matemática.
- **ANOVA de um fator (grupos étnicos):** diferenças significativas nas médias de matemática entre os cinco grupos, com os Grupos D e E apresentando os melhores resultados.

### Métricas de Erro e Tamanho de Efeito
Uma regressão linear simples foi ajustada entre leitura e escrita, gerando R² = 0,93 e REQM ≈ 5,4 pontos. O **d de Cohen** foi calculado para a diferença de gênero em matemática, resultando em ≈ 0,35 — classificado como efeito pequeno a médio, indicando que a diferença, embora significativa, tem impacto prático moderado.

---

## ⚙️ Como Executar

**1. Clone o repositório**
```bash
git clone https://github.com/seu-usuario/seu-repositorio.git
cd seu-repositorio
```

**2. Crie e ative o ambiente virtual**
```bash
python -m venv .venv

# Windows
.venv\Scripts\activate

# Linux / macOS
source .venv/bin/activate
```

**3. Instale as dependências**
```bash
pip install pandas numpy matplotlib seaborn scipy statsmodels jupyter
```

**4. Coloque o dataset na pasta raiz**

Baixe o arquivo `StudentsPerformance.csv` no [Kaggle](https://www.kaggle.com/datasets/spscientist/students-performance-in-exams) e salve na mesma pasta do notebook.

**5. Execute o notebook**
```bash
jupyter notebook analise_desempenho_alunos.ipynb
```

---

## 📁 Arquivos do Repositório

```
📦 repositorio
 ┣ 📓 analise_desempenho_alunos.ipynb   # Notebook principal com toda a análise
 ┣ 📄 StudentsPerformance.csv           # Dataset (deve ser baixado do Kaggle)
 ┗ 📄 README.md                         # Esta documentação
```

---

## 📚 Dataset

**Nome:** Students Performance in Exams  
**Fonte:** [Kaggle — Jakki Sathya Narayana](https://www.kaggle.com/datasets/spscientist/students-performance-in-exams)  
**Registros:** 1.000 alunos  
**Variáveis:** 8 (5 categóricas + 3 numéricas)

| Variável Original | Nome no Projeto | Tipo |
|---|---|---|
| gender | genero | Categórica |
| race/ethnicity | etnia | Categórica |
| parental level of education | escolaridade_pais | Categórica |
| lunch | almoco | Categórica |
| test preparation course | curso_preparatorio | Categórica |
| math score | nota_matematica | Numérica (0–100) |
| reading score | nota_leitura | Numérica (0–100) |
| writing score | nota_escrita | Numérica (0–100) |

---

## 🔎 Principais Conclusões

- Leitura e escrita têm correlação de Pearson r ≈ 0,96, indicando que se desenvolvem de forma conjunta.
- O **curso preparatório** eleva as notas em média 5 pontos em todas as disciplinas (efeito significativo com p << 0,001).
- O **tipo de almoço** (proxy de renda familiar) é o fator com maior associação ao desempenho em matemática.
- A **escolaridade dos pais** tem relação positiva com as notas — diferença de ~10 pontos entre extremos.
- **Gênero** influencia o desempenho por disciplina, mas com efeito de magnitude moderada (d de Cohen ≈ 0,35).
- **Grupos étnicos** apresentam diferenças significativas (ANOVA, p << 0,05), com Grupo E tendo a maior média.

---

<div align="center">
  Desenvolvido para a <strong>Asimov Jr</strong> — Semana 4
</div>
