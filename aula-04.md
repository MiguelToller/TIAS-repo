# Teoria do Pipeline de Aprendizado de Máquina Supervisionado

Em problemas de Aprendizado de Máquina Supervisionado onde as variáveis preditoras (**features**) e o rótulo a ser previso (**target**) já estão definidos, o processo de treinamento e validação segue um fluxo teórico padronizado para garantir a generalização do modelo.

---

## 🔄 Visão Geral do Pipeline Teórico

```
[Dados Brutos] 
       │
       ▼
[Limpeza e Imputação] 
       │
       ▼
[Separação: Features (X) vs Target (y)]
       │
       ▼
[Divisão: Base de Treino vs Base de Teste]
       │
       ▼
[Escalonamento de Features (Ajustado APENAS no Treino)]
       │
       ▼
[Treinamento do Algoritmo (Fit)]
       │
       ▼
[Avaliação do Desempenho (Métricas com Dados Inéditos)]

```

---

## 🧠 Etapas Fundamentais

### Etapa 1: Tratamento e Limpeza dos Dados

Antes da modelagem, a base de dados precisa ser higienizada:

* **Tratamento de Dados Ausentes:** Preenchimento de lacunas via imputação (média, mediana ou moda) ou remoção pontual dos registros incompletos.
* **Codificação Categórica:** Transformação de variáveis qualitativas (texto) em representações numéricas computáveis.

### Etapa 2: Isolamento de Features (X) e Target (y)

Diferenciação conceitual dos componentes do problema:

* **Features ($X$):** O conjunto de dados de entrada ou variáveis independentes usadas pelo algoritmo para identificar padrões.
* **Target ($y$):** A variável dependente (resposta) que o modelo tentará prever (por exemplo, uma classe binária $0$ ou $1$, ou um valor contínuo).

### Etapa 3: Divisão dos Dados e Prevenção de Contaminação

O conjunto de dados deve ser dividido em subconjuntos disjuntos para avaliar a capacidade do modelo de responder a dados desconhecidos:

* **Conjunto de Treino:** Utilizado exclusivamente para ajustar os parâmetros internos do algoritmo.
* **Conjunto de Teste:** Reservado para a validação final da capacidade de generalização.
* **Estratificação:** Garantia teórica de que a distribuição da variável alvo seja proporcionalmente idêntica nos subconjuntos de treino e teste.
* **Vazamento de Dados (*Data Leakage*):** Ocorre quando informações do conjunto de teste influenciam o treinamento ou o pré-processamento, resultando em métricas irrealistas.

### Etapa 4: Escalonamento e Normalização de Variáveis

Ajuste da amplitude das variáveis preditoras para garantir que diferenças nas escalas numéricas não afetem indevidamente os pesos do modelo:

* **Padronização ($Z$-Score):** Centralização dos dados em torno de média zero com desvio padrão unitário.
* **Princípio do Isolação:** Os parâmetros da padronização (como média e desvio padrão) devem ser calculados **apenas sobre os dados de treino**, sendo aplicados posteriormente ao conjunto de teste sem recalculá-los.

### Etapa 5: Treinamento do Modelo (Ajuste)

O algoritmo de aprendizado analisa a relação entre as features ($X$) e a variável alvo ($y$) do conjunto de treino:

* O objetivo primário é minimizar uma função de perda (*loss function*) interna do algoritmo escolhido.
* Algoritmos distintos utilizam estratégias variadas (por exemplo, hiperplanos em SVM, limites de decisão em Árvores, ou coeficientes em Regressão Logística).

### Etapa 6: Predição e Métricas de Avaliação

O modelo treinado recebe os dados de teste (sem revelar o alvo verdadeiro) para gerar predições, comparando as respostas com o target real:

#### Métricas de Classificação:

* **Acurácia:** Proporção geral de acertos sobre o total de predições.
* **Precision (Precisão):** Proporção de predições positivas que estavam corretas.
* **Recall (Revogação / Sensibilidade):** Proporção de instâncias positivas reais identificadas pelo modelo.
* **F1-Score:** Média harmônica entre Precisão e Recall, adequada para bases desbalanceadas.
* **Matriz de Confusão:** Tabela que detalha os acertos e erros categorizados em Verdadeiros Positivos, Verdadeiros Negativos, Falsos Positivos e Falsos Negativos.

---

## ⚡ AutoML e Validação Cruzada

* **Validação Cruzada (*K-Fold Cross-Validation*):** Técnica de reamostragem que divide a base de treino em múltiplos blocos ($K$ folds), alternando o bloco de teste interno. Garante estabilidade matemática à avaliação antes do teste final.
* **Ferramentas de AutoML (ex: PyCaret):** Abstraem conceitualmente o pipeline, executando sequencialmente a preparação dos dados, o dimensionamento, a validação cruzada e o ranqueamento automático de múltiplos algoritmos através das métricas selecionadas.
