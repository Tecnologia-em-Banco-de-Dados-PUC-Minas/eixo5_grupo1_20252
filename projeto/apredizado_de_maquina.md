# 🧠 Machine Learning por Base de Dados
**Bases:** Ambulatorial • Internações • Mortalidade

Este repositório documenta exclusivamente o **Machine Learning** aplicado às bases **Ambulatorial**, **Internações** e **Mortalidade**.  
A etapa de **ETL / feature engineering / dados** foi tratada anteriormente; aqui mantemos apenas os **artefatos de ML**:

- **Modelos** → catálogo dos **Modelos de Machine Learning** avaliados e escolhidos (descrições, configs, versões)
- **Códigos** → notebooks/scripts de ML (treino, validação, comparação)
- **Métricas** → resultados (tabelas, gráficos, relatórios)
- **Conclusões** → síntese das descobertas e decisões

Ambiente: **PySpark (Python)** em **Microsoft Fabric (Notebook/Lakehouse)** e **Google Colab**.

---

## 📚 Sumário — Artefatos de ML
- [Modelos de Machine Learning](#sum-modelos) — catálogo/versões & rationale
- [Códigos](#sum-codigos) — notebooks/scripts de treino e avaliação
- [Métricas](#sum-metricas) — resultados consolidados
- [Conclusões](#sum-conclusoes) — resumo interpretável para decisão

---

## 🗂️ Organização por Base de Dados
Cada **base** possui **quatro artefatos**:

| Base | Modelos | Códigos | Métricas | Conclusões |
|---|---|---|---|---|
| **Ambulatorial** | [`Ambulatorial/modelos/`](Ambulatorial/modelos/) | [`Ambulatorial/codigos/`](Ambulatorial/codigos/) | [`Ambulatorial/metricas/`](Ambulatorial/metricas/) | [`Ambulatorial/conclusoes/`](Ambulatorial/conclusoes/) |
| **Internações** | [`Internacoes/modelos/`](Internacoes/modelos/) | [`Internacoes/codigos/`](Internacoes/codigos/) | [`Internacoes/metricas/`](Internacoes/metricas/) | [`Internacoes/conclusoes/`](Internacoes/conclusoes/) |
| **Mortalidade** | [`Mortalidade/modelos/`](Mortalidade/modelos/) | [`Mortalidade/codigos/`](Mortalidade/codigos/) | [`Mortalidade/metricas/`](Mortalidade/metricas/) | [`Mortalidade/conclusoes/`](Mortalidade/conclusoes/) |

## 🗂️ Organização por Base de Dados


---

<details>
  <summary><b>Ambulatorial</b></summary>

**Artefatos**
- **Modelos** → catálogo e configs dos modelos avaliados: [`Ambulatorial/modelos/`](Ambulatorial/modelos/)
- **Códigos** → notebooks/scripts de ML: [`Ambulatorial/codigos/`](Ambulatorial/codigos/)
- **Métricas** → resultados e gráficos: [`Ambulatorial/metricas/`](Ambulatorial/metricas/)
- **Conclusões** → resumo interpretável: [`Ambulatorial/conclusoes/`](Ambulatorial/conclusoes/)

<pre><code>Ambulatorial
 ├─ modelos/
 │   ├─ 00_catalogo.md
 │   ├─ logreg.yaml
 │   ├─ random_forest.yaml
 │   └─ gbt_spark.yaml
 ├─ codigos/
 │   ├─ 01_treinamento_modelos_ml.ipynb
 │   ├─ 02_avaliacao_modelos_ml.ipynb
 │   └─ utils_ml.py
 ├─ metricas/
 │   ├─ resultados_ambulatorial.csv
 │   ├─ matriz_confusao.png
 │   └─ curvas_roc_pr.png
 └─ conclusoes/
     └─ README.md
</code></pre>
</details>

---

<details>
  <summary><b>Internações</b></summary>

**Artefatos**
- **Modelos** → catálogo e configs: [`Internacoes/modelos/`](Internacoes/modelos/)
- **Códigos** → notebooks/scripts de ML: [`Internacoes/codigos/`](Internacoes/codigos/)
- **Métricas** → resultados e gráficos: [`Internacoes/metricas/`](Internacoes/metricas/)
- **Conclusões** → resumo interpretável: [`Internacoes/conclusoes/`](Internacoes/conclusoes/)

<pre><code>Internacoes
 ├─ modelos/
 │   ├─ 00_catalogo.md
 │   ├─ logreg.yaml
 │   ├─ random_forest.yaml
 │   └─ gbt_spark.yaml
 ├─ codigos/
 │   ├─ 01_treinamento_modelos_ml.ipynb
 │   ├─ 02_avaliacao_modelos_ml.ipynb
 │   └─ utils_ml.py
 ├─ metricas/
 │   ├─ resultados_internacoes.csv
 │   ├─ matriz_confusao.png
 │   └─ curvas_roc_pr.png
 └─ conclusoes/
     └─ README.md
</code></pre>
</details>

---

<details>
  <summary><b>Mortalidade</b></summary>

**Artefatos**
- **modelos/** → catálogo e configs: [`Mortalidade/modelos/`](Mortalidade/modelos/)
- **codigos/** → notebooks/scripts de ML: [`Mortalidade/codigos/`](Mortalidade/codigos/)
- **metricas/** → resultados e gráficos: [`Mortalidade/metricas/`](Mortalidade/metricas/)
- **conclusoes/** → resumo interpretável: [`Mortalidade/conclusoes/`](Mortalidade/conclusoes/)

<pre><code>Mortalidade
 ├─ modelos/
 │   ├─ 00_catalogo.md
 │   ├─ logreg.yaml
 │   ├─ random_forest.yaml
 │   └─ gbt_spark.yaml
 ├─ codigos/
 │   ├─ 01_treinamento_modelos_ml.ipynb
 │   ├─ 02_avaliacao_modelos_ml.ipynb
 │   └─ utils_ml.py
 ├─ metricas/
 │   ├─ resultados_mortalidade.csv
 │   ├─ matriz_confusao.png
 │   └─ curvas_roc_pr.png
 └─ conclusoes/
     └─ README.md
</code></pre>
</details>


