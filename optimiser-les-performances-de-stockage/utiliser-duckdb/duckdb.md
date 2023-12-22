# 👩🏫 DuckDB

## Qu'est-ce que DuckDB ?

Il s'agit d'une base de données qui fonctionne comme un processus. Elle ne possède pas de serveur dédié comme une [base SQL](../utiliser-une-base-sql/). Elle fait effectuer directement le traitement de lecture par le logiciel support qui effectue les calculs. Elle se rapproche de SQLite avec une orientation forte sur l'analyse de données.

### Les avantages de cette base de données

* Elle préserve la simplicité du travail sur un seul fichier
* Elle permet d'utiliser la précision et la richesse des dernières versions de SQL pour la lecture
* Elle est très efficace pour l'analyse, car elle est capable d'interroger un fichier[ Parquet](../utiliser-parquet.md) de façon très peu couteuse (travail sur disque qui libère la RAM pour les calculs et le DataFrame R ou Python).

### Les défauts de cette base de données

* Elle n'est pas optimisée pour les opérations transactionnelles (comme Parquet), il est préférable d'utiliser un SGBD traditionnel pour cela.

## Mettre en place une base DuckDB

Vous pouvez [mettre en place duckDB](https://duckdb.org/docs/api/overview) de manière très simple avec beaucoup de clients différents ! Pour vous aider, voici des exemples commentés en français  :&#x20;

* Comment mettre en place [DuckDB en R](duckdb-avec-r.md)
* Comment mettre en place[ DuckDB en Python](duckdb-avec-python.md)
