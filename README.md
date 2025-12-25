# Projeto de Triagem de Transtorno do Espectro do Autismo (TEA) com Machine Learning

## Descrição do Projeto

Este projeto de **Análise de Dados e Machine Learning** tem como objetivo desenvolver um modelo de classificação para auxiliar na triagem de indivíduos com potencial Transtorno do Espectro do Autismo (TEA). Utilizando um conjunto de dados baseado em questionários de triagem e informações demográficas, o projeto explora as etapas de limpeza, pré-processamento, análise exploratória de dados (EDA) e modelagem preditiva.

O foco principal é identificar os fatores mais preditivos para o resultado da triagem, fornecendo *insights* valiosos sobre a relação entre as respostas do questionário, variáveis demográficas e a classificação final.

## Tecnologias e Bibliotecas

O projeto foi desenvolvido em Python e utiliza as seguintes bibliotecas:

| Categoria | Biblioteca | Uso Principal |
| :--- | :--- | :--- |
| **Manipulação de Dados** | `pandas`, `numpy` | Limpeza, pré-processamento e estruturação do conjunto de dados. |
| **Visualização de Dados** | `matplotlib`, `seaborn` | Análise Exploratória de Dados (EDA), incluindo histogramas, boxplots e matriz de correlação. |
| **Machine Learning** | `scikit-learn` | Implementação do modelo de Classificação por Árvore de Decisão e avaliação de métricas. |

## Estrutura do Repositório

O repositório está organizado nas seguintes pastas:

| Diretório | Conteúdo |
| :--- | :--- |
| `Data/` | Contém o conjunto de dados brutos e/ou processados utilizados no projeto. |
| `Notebooks/` | Contém o principal *Jupyter Notebook* com todo o fluxo de trabalho do projeto. |
| `README.md` | Este arquivo. |

O fluxo de trabalho completo do projeto pode ser encontrado no *notebook* principal: `Notebooks/autism_screening.ipynb`.

## Análise Exploratória de Dados (EDA) e Pré-processamento

A fase de EDA revelou características importantes do conjunto de dados que influenciaram a modelagem:

1.  **Limpeza e Codificação:** Foram realizados o tratamento de valores ausentes (especialmente na coluna `age`, substituindo *outliers* e nulos pela mediana) e a codificação de variáveis categóricas. Variáveis como `gender`, `jaundice` (icterícia) e `austim` (histórico familiar) foram transformadas em binárias, enquanto a `ethnicity` foi tratada com *One-Hot Encoding*.
2.  **Desbalanceamento de Classes:** A análise da variável alvo (`class_asd`) indicou um desbalanceamento, com a maioria dos indivíduos classificados como "Não" (0) na triagem.
3.  **Fatores Preditivos Chave:**
    *   **Pontuação Total (`result`):** A pontuação total obtida no questionário demonstrou a maior correlação positiva (0.82) com o resultado final da triagem.
    *   **Histórico Familiar (`austim`):** A presença de histórico familiar de autismo (`austim = 1`) é um preditor extremamente forte, aumentando significativamente a proporção de resultados positivos.
    *   **Perguntas Individuais:** As perguntas do questionário relacionadas à **cognição e percepção social** (como `A9_Score`, `A5_Score`, `A6_Score` e `A4_Score`) se destacaram como os indicadores individuais mais influentes para a classificação.

## Modelagem de Classificação

Para a classificação, foi implementado um modelo de **Árvore de Decisão** (`DecisionTreeClassifier`) com o objetivo de prever o resultado da triagem (`class_asd`).

O modelo foi treinado com os seguintes hiperparâmetros, incluindo o balanceamento de classes (`class_weight='balanced'`) para mitigar o desbalanceamento identificado na EDA:

*   **Modelo:** `DecisionTreeClassifier`
*   **Profundidade Máxima (`max_depth`):** 5
*   **Critério de Divisão (`criterion`):** 'entropy'
*   **Balanceamento de Classes:** 'balanced'

### Resultados da Avaliação

A avaliação do modelo no conjunto de teste (30% dos dados) resultou nas seguintes métricas:

| Métrica | Valor |
| :--- | :--- |
| **Acurácia** | 1.0 |
| **Precisão** | 1.0 |
| **Recall** | 1.0 |
| **F1-Score** | 1.0 |

**Nota sobre os Resultados:** As métricas de 1.0 em todas as categorias sugerem um desempenho perfeito no conjunto de teste. No entanto, a visualização da Árvore de Decisão revela que o modelo utiliza o `result` (pontuação total) como o principal nó de decisão. Isso indica que o modelo está aprendendo a regra de pontuação subjacente do questionário, o que pode levar a um *overfitting* ou a uma simplificação excessiva do problema. Em um cenário real, seria recomendável testar o modelo em um conjunto de dados completamente novo ou remover a coluna `result` para forçar o modelo a aprender padrões mais complexos a partir das respostas individuais (A1-A10) e variáveis demográficas.

## Como Executar o Projeto

Para replicar a análise e a modelagem, siga os passos abaixo:

1.  **Clone o Repositório:**
    ```bash
    git clone https://github.com/theusnevess/triagem-autismo.git
    cd triagem-autismo
    ```

2.  **Instale as Dependências:**
    Certifique-se de ter o Python instalado. As bibliotecas necessárias podem ser instaladas via `pip`:
    ```bash
    pip install pandas numpy matplotlib seaborn scikit-learn
    ```

3.  **Execute o Notebook:**
    Abra o arquivo `Notebooks/autism_screening.ipynb` em um ambiente Jupyter (Jupyter Notebook, JupyterLab ou VS Code) e execute as células sequencialmente.

## Contato

Para dúvidas, sugestões ou colaborações, entre em contato com o autor do repositório:
