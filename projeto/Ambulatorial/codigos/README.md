# Ambulatorial — Códigos (ML)
Coloque aqui notebooks/scripts de treino/avaliação.

## Sugerido
- `01_treinamento_modelos_ml.ipynb`
- `02_avaliacao_modelos_ml.ipynb`
- `utils_ml.py`

## Exemplo (Colab)
```python
!pip install -q pyspark==3.5.1
from pyspark.sql import SparkSession
spark = (SparkSession.builder.appName("Saude-ML").getOrCreate())
```
