<div align="center">

# Zomato Data Pipeline

### End-to-end data engineering with AI-powered analytics.

An end-to-end data pipeline that processes Zomato datasets using Amazon S3, Snowflake, dbt, and Apache Airflow. Implements medallion architecture for data transformation and integrates AI-powered review insights, RAG-based question answering, and natural-language-to-SQL analytics.

<p>
  <img src="https://img.shields.io/badge/Python-Data_Processing-3776AB?style=for-the-badge&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/Amazon_S3-Data_Storage-569A31?style=for-the-badge&logo=amazons3&logoColor=white" />
  <img src="https://img.shields.io/badge/Snowflake-Data_Warehouse-29B5E8?style=for-the-badge&logo=snowflake&logoColor=white" />
  <img src="https://img.shields.io/badge/dbt-Data_Transformation-FF694B?style=for-the-badge&logo=dbt&logoColor=white" />
  <img src="https://img.shields.io/badge/Apache_Airflow-Orchestration-017CEE?style=for-the-badge&logo=apacheairflow&logoColor=white" />
  <img src="https://img.shields.io/badge/OpenAI-AI_Integration-412991?style=for-the-badge&logo=openai&logoColor=white" />
</p>

</div>

---

## About the Project

The Zomato Data Pipeline transforms seven raw CSV datasets into structured, analytics-ready data using Amazon S3, Snowflake, and dbt.

The project follows a medallion architecture, organizing data into staging models, dimensions, fact tables, and analytical marts. Apache Airflow orchestrates the daily workflow, while OpenAI powers review enrichment, document-grounded question answering, and natural-language SQL queries.

The processed data can be explored through Streamlit and Snowflake Snowsight.

## Features

- **Data Ingestion:** Load seven raw CSV datasets into Amazon S3.
- **Cloud Data Warehouse:** Ingest data into Snowflake using `COPY INTO` and storage integration.
- **Medallion Architecture:** Organize transformations into staging models and analytical marts.
- **Data Transformation:** Use dbt to build staging views, dimensions, fact tables, and aggregate marts.
- **Workflow Orchestration:** Automate ingestion, dbt transformations, and AI enrichment using Apache Airflow.
- **AI Review Enrichment:** Generate structured summaries and insights from customer reviews using OpenAI.
- **RAG-Based Q&A:** Answer questions about customer reviews using retrieved context.
- **Natural Language to SQL:** Convert natural-language questions into SQL queries against analytical tables.
- **Data Visualization:** Explore analytical results through Streamlit and Snowsight.
- **Automated Pipeline:** Run the daily data processing workflow through an Airflow DAG.

## Tech Stack

| Technology     | Purpose                                       |
| -------------- | --------------------------------------------- |
| Python         | Data processing and AI integration            |
| Pandas         | CSV processing and data manipulation          |
| Amazon S3      | Raw data storage                              |
| Snowflake      | Cloud data warehouse                          |
| SQL            | Data querying and analysis                    |
| dbt            | Data transformation and modeling              |
| Apache Airflow | Workflow orchestration                        |
| OpenAI API     | AI-powered review analysis and SQL generation |
| Streamlit      | Interactive analytics interface               |
| Snowsight      | Snowflake data exploration                    |
| Docker         | Containerized development environment         |

## How It Works

1. **Data Ingestion:** Upload seven raw CSV datasets to Amazon S3.
2. **Warehouse Loading:** Load the datasets into Snowflake using `COPY INTO` and storage integration.
3. **Data Transformation:** Use dbt to clean and transform raw data into staging models.
4. **Analytical Modeling:** Build dimensions, fact tables, and aggregate marts for business analytics.
5. **AI Enrichment:** Process customer reviews using OpenAI and store the generated insights.
6. **Workflow Orchestration:** Run the ingestion, transformation, and enrichment tasks through an Apache Airflow DAG.
7. **Analytics:** Explore business metrics, review insights, and query results through Streamlit and Snowsight.

## Architecture

```text
        Raw CSV Datasets
        (7 Datasets)
              |
              v
          Amazon S3
         Raw Storage
              |
              v
          Snowflake
         RAW Tables
              |
              v
             dbt
      Staging Models
              |
              v
      Dimensions & Facts
              |
              v
       Analytical Marts
              |
       +------+------+
       |             |
       v             v
   Streamlit      Snowsight
    Analytics     Exploration


       Apache Airflow
              |
     +--------+---------+
     |        |         |
     v        v         v
   S3 Load  dbt Build  AI Enrichment
                         |
                         v
                  Review Insights
                         |
                         v
                   Analytical Marts


       OpenAI Integration
              |
      +-------+--------+
      |                |
      v                v
  RAG-Based Q&A   Natural Language
                  to SQL Queries
```

## Data Models

### Staging Models

The staging layer prepares raw data for downstream transformations.

- `stg_food.sql`
- `stg_menu.sql`
- `stg_orders.sql`
- `stg_restaurants.sql`
- `stg_reviews.sql`
- `stg_users.sql`

### Analytical Marts

The marts layer provides structured datasets for business analysis.

- `fact_orders.sql` — Order-level analytical data.
- `dim_customer.sql` — Customer dimension.
- `mart_daily_city_revenue.sql` — Daily revenue aggregated by city.
- `mart_delivery_sla.sql` — Delivery performance analysis.
- `mart_review_insights` — AI-enriched customer review insights.

## AI Capabilities

### 1. Review Enrichment

Uses OpenAI to process customer reviews and generate structured summaries and insights, which are stored in Snowflake for analysis.

### 2. RAG-Based Review Q&A

Retrieves relevant review information to answer natural-language questions grounded in customer feedback.

### 3. Natural Language to SQL

Converts natural-language questions into SQL queries against the analytical marts. Includes a SELECT-only guard and restricted database permissions through `DBT_ROLE`.

## Workflow Orchestration

Apache Airflow orchestrates the daily pipeline using the `zomato_batch.py` DAG.

The workflow includes:

1. `upload_raw` — Upload raw datasets to Amazon S3.
2. `dbt_build_core` — Build core dbt models.
3. `enrich_reviews` — Generate AI-powered review insights.
4. `dbt_build_all` — Build the remaining models and analytical marts.

## Getting Started

### Prerequisites

- Python
- AWS account and Amazon S3 bucket
- Snowflake account
- dbt with the Snowflake adapter
- Apache Airflow
- OpenAI API key
- Docker, if required by the project environment

### 1. Clone the Repository

```bash
git https://github.com/Dewanshu-Chirkhe/Zomato-Data-Pipeline
cd Zomato-Data-Pipeline
```

### 2. Configure Environment Variables

Configure the credentials and connection settings required by your application.

```env
AWS_ACCESS_KEY_ID=your_aws_access_key
AWS_SECRET_ACCESS_KEY=your_aws_secret_key
AWS_DEFAULT_REGION=your_aws_region
S3_BUCKET_NAME=your_bucket_name

SNOWFLAKE_ACCOUNT=your_account
SNOWFLAKE_USER=your_username
SNOWFLAKE_PASSWORD=your_password
SNOWFLAKE_DATABASE=your_database
SNOWFLAKE_SCHEMA=your_schema
SNOWFLAKE_WAREHOUSE=your_warehouse
SNOWFLAKE_ROLE=your_role

OPENAI_API_KEY=your_openai_api_key
```

Use the exact environment variable names defined in your project configuration. Never commit credentials to GitHub.

### 3. Configure dbt

Configure your Snowflake connection in the dbt profile and verify that the project can connect to your warehouse.

```bash
dbt debug
```

### 4. Run dbt Models

```bash
dbt run
```

To execute data quality tests, if configured:

```bash
dbt test
```

### 5. Run the Pipeline

Configure and start Airflow, then trigger the `zomato_batch.py` DAG from the Airflow interface or CLI.

Run the AI scripts and Streamlit application using the commands and configuration defined in your repository.

## What I Learned

- Building end-to-end data engineering pipelines.
- Ingesting data from Amazon S3 into Snowflake.
- Designing medallion architecture with dbt.
- Creating fact tables, dimensions, and analytical marts.
- Automating data workflows using Apache Airflow.
- Integrating OpenAI into data analytics workflows.
- Implementing RAG-based question answering over customer reviews.
- Generating SQL from natural-language questions with query restrictions.
- Presenting analytical results through Streamlit and Snowsight.

---

<div align="center">

**Zomato Data Pipeline** — From raw datasets to AI-powered analytics.

Built with Python, Amazon S3, Snowflake, dbt, Apache Airflow, and OpenAI.

</div>
