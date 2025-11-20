# 📉 Projeto: Análise de Evasão de Clientes (Churn) na Telecom X

## 🎯 1. Propósito da Análise

Este projeto visa realizar uma **Análise Exploratória de Dados (EDA)** detalhada sobre a base de clientes da **Telecom X** para identificar os fatores, padrões e perfis de clientes que levam à **evasão (Churn)**.

O objetivo final é transformar dados brutos (JSON de API) em **insights acionáveis** que servirão de base para:
* **Decisão Estratégica:** Direcionar esforços de marketing e produto para grupos de risco.
* **Modelagem Preditiva:** Fornecer dados limpos e *features* relevantes para a construção de modelos de previsão de Churn mais precisos.

## 📁 2. Estrutura do Projeto e Organização dos Arquivos

O projeto está organizado na seguinte estrutura de diretórios, garantindo clareza e separação de responsabilidades:

* **`analise_churn_telecomx.ipynb`**: O notebook principal onde todas as etapas do projeto são executadas: **ETL**, **EDA** e **Relatório Final** (em células Markdown e de código).
* **`README.md`**:
    * Documentação, com o propósito e as instruções de uso
    * Contém a documentação final, conclusões e recomendações do projeto.

## 📊 3. Exemplos de Gráficos e Insights Obtidos

A EDA revelou padrões claros de alto risco de evasão, sendo os contratos de **Mês a Mês** e a **baixa fidelidade (`tenure`)** os principais preditores de Churn.

### A. Distribuição da Evasão por Contrato
O gráfico de barras segmentadas mostra que clientes com contratos mensais têm uma taxa de Churn dramaticamente maior.



**Insight Chave:** O contrato **Mês a Mês** tem a **maior taxa de Churn** (geralmente acima de 40%), exigindo intervenção imediata para migração ou incentivo à fidelização.

### B. Distribuição de Tempo de Contrato (`Tenure`)
O Box Plot compara o tempo de contrato entre clientes que cancelaram e os que ficaram.



**Insight Chave:** A **mediana de `tenure`** para clientes que evadiram (`Yes`) está concentrada nos **primeiros meses de serviço**, indicando a necessidade de um foco maior no programa de *onboarding* (acolhimento inicial).

## 💻 4. Instruções para Executar o Notebook

Para replicar a análise e gerar os resultados, siga os passos abaixo:

### Ambiente de Execução
O notebook foi desenvolvido para ser executado primariamente no **Google Colab**, pois utiliza um ambiente Python pré-configurado e facilita o compartilhamento e a execução de bibliotecas de Data Science.

### Pré-requisitos
Certifique-se de ter acesso à internet e uma conta Google (para o Colab). Alternativamente, você pode usar um ambiente Jupyter local.

### Dependências
As bibliotecas necessárias serão instaladas automaticamente no Colab. Se estiver executando localmente, instale-as via pip:

```bash
pip install pandas numpy matplotlib seaborn requests
```


# 📉 Relatório Final: Análise de Evasão de Clientes (Churn) - Telecom X

## 1. Introdução

O presente relatório resume os achados da Análise Exploratória de Dados (EDA) conduzida sobre a base de clientes da Telecom X. Este projeto foi desenvolvido e executado no ambiente **Google Colab**, garantindo a fácil replicação e portabilidade do código.

O objetivo principal é **entender os fatores que influenciam a evasão (Churn)**, fornecendo *insights* acionáveis para a equipe de Data Science e para a formulação de estratégias de retenção. A taxa de Churn observada na base de dados é de aproximadamente **26.5%**, indicando um problema crítico.

## 2. Limpeza e Tratamento de Dados (ETL)

A fase inicial de **Extração, Transformação e Carga (ETL)** foi fundamental para garantir a qualidade dos dados:

1.  **Extração da API e Normalização:** Os dados foram obtidos através de uma **simulação de requisição HTTP GET** usando a biblioteca **`requests`**, imitando a integração com o *endpoint* da API da Telecom X. A resposta, em formato JSON aninhado, foi processada utilizando o `pd.json_normalize` para achatar as estruturas hierárquicas, resultando em um DataFrame plano.
2.  **Correção de Tipos e Tratamento de Nulos:**
    * A coluna **`account.Charges.Total`** foi identificada incorretamente como `object` (string).
    * **Ação:** Foi convertida para o tipo numérico (`float64`) e os valores nulos resultantes (provenientes de clientes com `tenure = 0`) foram preenchidos com **0.0**.

## 3. Análise Exploratória de Dados (EDA)

### 3.1. Distribuição da Variável Alvo (`Churn`)

O *dataset* apresenta um desbalanceamento: ~73.5% dos clientes não evadiram (`No`) e **~26.5% evadiram (`Yes`)**.

### 3.2. Análise por Variáveis Categóricas

A taxa de evasão é fortemente influenciada pelas seguintes categorias:

| Variável | Fator de Alto Risco | Taxa de Evasão |
| :--- | :--- | :--- |
| **Contrato** | **Mês a Mês** | Maior que 40% |
| **Serviços Adicionais** | **Não ter Segurança Online/Suporte Técnico** | Significativamente maior que a média |

### 3.3. Análise por Variáveis Numéricas

A comparação das distribuições (Box Plots) revelou:

1.  **Tempo de Contrato (`tenure`):** A **mediana** de `tenure` para clientes que evadiram é **muito mais baixa**, indicando que a evasão ocorre nos primeiros meses.
2.  **Gastos Mensais (`Charges.Monthly`):** Clientes que evadem possuem uma **mediana de gastos mensais superior** aos clientes que permanecem.

## 4. Conclusões e Recomendações

### 4.1. Conclusão Principal

O perfil do cliente com maior risco de Churn é: **recém-chegado**, com contrato **Mês a Mês**, gastando um **valor mensal alto** e **sem serviços de segurança** que justifiquem o preço.

### 4.2. Recomendações Estratégicas

1.  **Foco em Onboarding (Primeiros Meses):** Implementar um programa de retenção intensivo nos **primeiros 3 a 6 meses** de contrato.
2.  **Promoção de Fidelidade:** Oferecer incentivos para que clientes **Mês a Mês** migrem para contratos de 1 ou 2 anos.
3.  **Aumento da Barreira de Saída:** Promover os serviços de **Segurança Online** e **Suporte Técnico** para clientes de alto risco.
