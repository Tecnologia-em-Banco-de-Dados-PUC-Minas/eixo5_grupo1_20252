# 🧠 Machine Learning por Base de Dados
**Bases:** Ambulatorial • Internações • Mortalidade

Este repositório documenta exclusivamente o **Machine Learning** aplicado sobre três bases de dados de saúde:
**Ambulatorial**, **Internações** e **Mortalidade**.  
A etapa de **ETL / feature engineering / dados** foi tratada anteriormente; aqui mantemos apenas os **artefatos de ML**:
**códigos**, **métricas** e **conclusões**.

- Linguagem/Framework: **PySpark (Python)**
- Ambiente suportado: **Microsoft Fabric (Lakehouse / Notebook)** e **Google Colab (Notebook)**

---

## 📚 Sumário
- [Organização por Base de Dados](#-organização-por-base-de-dados)
- [Como Executar](#-como-executar)
  - [Google Colab](#opção-a-google-colab)
  - [Microsoft Fabric](#opção-b-microsoft-fabric)
- [Padrões e Convenções](#-padrões-e-convenções)
- [Templates Úteis](#-templates-úteis)
- [Contribuição](#-contribuição)
- [Licença](#-licença)

---

## 🗂️ Organização por Base de Dados
Cada **base de dados** possui três **artefatos de ML**:

- **codigos/** → notebooks/scripts de ML (treino, validação, comparação de modelos)
- **metricas/** → resultados (tabelas, gráficos, relatórios)
- **conclusoes/** → síntese das descobertas e decisões (interpretável para stakeholders)

| Base de dados | Códigos (ML) | Métricas | Conclusões |
|---|---|---|---|
| **Ambulatorial** | [`Ambulatorial/codigos/`](Ambulatorial/codigos/) | [`Ambulatorial/metricas/`](Ambulatorial/metricas/) | [`Ambulatorial/conclusoes/`](Ambulatorial/conclusoes/) |
| **Internações** | [`Internacoes/codigos/`](Internacoes/codigos/) | [`Internacoes/metricas/`](Internacoes/metricas/) | [`Internacoes/conclusoes/`](Internacoes/conclusoes/) |
| **Mortalidade** | [`Mortalidade/codigos/`](Mortalidade/codigos/) | [`Mortalidade/metricas/`](Mortalidade/metricas/) | [`Mortalidade/conclusoes/`](Mortalidade/conclusoes/) |

<details>
  <summary><b>Ambulatorial — artefatos de ML</b></summary>

- **Códigos (ML):** [`Ambulatorial/codigos/`](Ambulatorial/codigos/)  
  Notebooks/scripts de treino, validação, comparação de modelos e exportação de previsões.
- **Métricas:** [`Ambulatorial/metricas/`](Ambulatorial/metricas/)  
  CSV/PNG/HTML com AUC, F1, ACC, matriz de confusão, curvas ROC/PR, calibração etc.
- **Conclusões:** [`Ambulatorial/conclusoes/`](Ambulatorial/conclusoes/)  
  Síntese das descobertas, modelo escolhido, limiares e próximos passos.

</details>

<details>
  <summary><b>Internações — artefatos de ML</b></summary>

- **Códigos (ML):** [`Internacoes/codigos/`](Internacoes/codigos/)  
- **Métricas:** [`Internacoes/metricas/`](Internacoes/metricas/)  
- **Conclusões:** [`Internacoes/conclusoes/`](Internacoes/conclusoes/)

</details>

<details>
  <summary><b>Mortalidade — artefatos de ML</b></summary>

- **Códigos (ML):** [`Mortalidade/codigos/`](Mortalidade/codigos/)  
- **Métricas:** [`Mortalidade/metricas/`](Mortalidade/metricas/)  
- **Conclusões:** [`Mortalidade/conclusoes/`](Mortalidade/conclusoes/)

</details>

> **Observação técnica:** se os fences (\`\`\`) dentro de `<details>` ficarem em **uma linha só** no preview, troque por `<pre><code> ... </code></pre>`.

---

## 🚀 Como Executar

### Opção A) Google Colab
```python
# Dependências mínimas
!pip install -q pyspark==3.5.1

from pyspark.sql import SparkSession
spark = (SparkSession.builder.appName("Saude-ML").getOrCreate())

# Exemplo de leitura de base (ajuste o caminho conforme sua organização)
df = spark.read.parquet("data/ambulatorial/processed/*.parquet")
df.printSchema()
