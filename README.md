# workshop_airflow

Ambiente de estudo do Apache Airflow (via Astro CLI) com pipelines de ingestão e processamento de dados de preço do Bitcoin, cobrindo extração de API, carga em Postgres e submissão de jobs Spark.

## O que o projeto faz

- **`bitcoin_price_dag`**: extrai o preço atual do Bitcoin (API CoinGecko) usando a TaskFlow API e carrega em uma tabela Postgres
- **`bitcoin_bronze_ingestion`**: ingestão horizontal (camada bronze) do preço, market cap e volume do Bitcoin, rodando de hora em hora
- **`bitcoin_spark_pipeline`**: dispara um job Spark remoto (`spark-submit` em modo cluster) para processar os dados ingeridos

## Stack

- [Apache Airflow](https://airflow.apache.org/) (TaskFlow API) via [Astro CLI](https://www.astronomer.io/docs/astro/cli/overview)
- PostgreSQL (armazenamento)
- Apache Spark (processamento)
- Docker (ambiente local do Airflow)

## Como rodar

1. Instale a [Astro CLI](https://www.astronomer.io/docs/astro/cli/install-cli)
2. Suba o ambiente local:
   ```bash
   astro dev start
   ```
3. Acesse a UI do Airflow em `http://localhost:8080`
4. Configure a conexão `postgres_local` no Airflow (Admin > Connections) apontando para seu Postgres
5. Ative as DAGs `bitcoin_price_taskflow` e `bitcoin_bronze_ingestion`

## Estrutura

```
dags/       # DAGs de ingestão e pipeline
include/    # jobs Spark e demais arquivos auxiliares
```
