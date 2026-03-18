# 🚀 Airflow ETL Pipeline: NASA APOD to Postgres

Dive into the cosmos with this robust ETL pipeline that seamlessly extracts, transforms, and loads NASA's Astronomy Picture of the Day data into a PostgreSQL database using Apache Airflow's powerful orchestration capabilities.

## 🌟 Project Overview

This project showcases a modern ETL (Extract, Transform, Load) pipeline built with Apache Airflow, designed to fetch captivating astronomical data from NASA's Astronomy Picture of the Day (APOD) API, process it efficiently, and store it in a PostgreSQL database. By leveraging Docker for containerization, we ensure a portable, isolated environment that runs smoothly across different systems.

The pipeline demonstrates best practices in data engineering, utilizing Airflow's hooks and operators for reliable, scheduled data workflows that can scale with your needs.

## 🏗️ Key Components

### 🌬️ Apache Airflow for Orchestration

- **Workflow Management**: Airflow defines and schedules the entire ETL pipeline as a Directed Acyclic Graph (DAG), ensuring tasks execute in the correct order with proper dependencies.
- **Monitoring & Scheduling**: Built-in web UI for real-time monitoring, task retries, and flexible scheduling (daily runs in this case).
- **TaskFlow API**: Modern Pythonic approach using decorators for clean, readable task definitions.

### 🐘 PostgreSQL Database

- **Data Storage**: Robust relational database for storing transformed astronomical data.
- **Docker Integration**: Containerized Postgres with persistent volumes for data durability.
- **Airflow Integration**: Seamless interaction via PostgresHook and PostgresOperator for efficient database operations.

### 🌌 NASA APOD API

- **Data Source**: Rich astronomical content including daily images, titles, explanations, and metadata.
- **HTTP Operations**: Leveraged through Airflow's SimpleHttpOperator for reliable API interactions.
- **JSON Processing**: Handles structured API responses with ease.

## 🎯 Project Objectives

### 📥 Extract

- **Automated Fetching**: Daily scheduled extraction of fresh astronomical data from NASA's APOD API.
- **Reliable Requests**: Robust HTTP handling with proper error management and retries.

### 🔄 Transform

- **Data Processing**: Intelligent parsing and cleaning of API responses.
- **Format Optimization**: Ensures data compatibility with database schema requirements.
- **Quality Assurance**: Validation and standardization of fields like title, explanation, URL, and date.

### 📤 Load

- **Database Integration**: Efficient insertion of transformed data into PostgreSQL.
- **Schema Management**: Automatic table creation if needed, with proper indexing for performance.
- **Data Persistence**: Secure storage enabling downstream analytics and reporting.

## 🏛️ Architecture & Workflow

Our ETL pipeline follows a clean, three-stage architecture orchestrated through Airflow:

```
🌐 NASA APOD API → 📊 Extract → 🔄 Transform → 🗄️ Load → 🐘 PostgreSQL
```

### 1. Extract Stage

- **SimpleHttpOperator**: Makes authenticated GET requests to NASA's APOD endpoint.
- **JSON Response Handling**: Captures rich metadata including image URLs, descriptions, and astronomical context.
- **Error Resilience**: Built-in retry mechanisms for API reliability.

### 2. Transform Stage

- **TaskFlow Processing**: Python-based transformation using Airflow's `@task` decorator.
- **Data Refinement**: Extracts key fields (title, explanation, URL, date) and applies formatting.
- **Validation**: Ensures data integrity before database insertion.

### 3. Load Stage

- **PostgresHook Integration**: Direct database connectivity for efficient data loading.
- **Dynamic Schema**: Automatic table creation with appropriate data types.
- **Batch Operations**: Optimized insertion for performance and reliability.

## 🚀 Getting Started

### Prerequisites

- Docker & Docker Compose
- Git
- Basic understanding of containerized workflows

### Quick Setup

1. **Clone the Repository**

   ```bash
   git clone <repository-url>
   cd etl-pipeline
   ```

2. **Launch the Environment**

   ```bash
   docker-compose up -d
   ```

3. **Access Airflow UI**
   - Navigate to `http://localhost:8080`
   - Default credentials: admin/admin

4. **Trigger the Pipeline**
   - Enable the DAG in the Airflow web interface
   - Watch the magic happen!

### Configuration

- **API Key**: Obtain a NASA API key from [NASA's API Portal](https://api.nasa.gov/)
- **Environment Variables**: Configure database connections and API credentials
- **Scheduling**: Adjust DAG schedule intervals as needed

## 📊 Data Schema

The pipeline creates a `apod_data` table with the following structure:

| Column      | Type         | Description              |
| ----------- | ------------ | ------------------------ |
| id          | SERIAL       | Primary key              |
| title       | VARCHAR(255) | Image title              |
| explanation | TEXT         | Astronomical explanation |
| url         | TEXT         | Image URL                |
| date        | DATE         | APOD date                |
| media_type  | VARCHAR(50)  | Media type (image/video) |

## 🔧 Development & Testing

### Testing Suite

- Unit tests for transformation logic
- Integration tests for API and database interactions
- DAG validation tests

### Local Development

```bash
# Run tests
docker-compose exec airflow-webserver python -m pytest tests/

# Access database
docker-compose exec postgres psql -U airflow -d apod_db
```

## 🤝 Contributing

We welcome contributions! Whether it's:

- 🐛 Bug fixes
- ✨ New features
- 📚 Documentation improvements
- 🧪 Additional tests

Please submit a pull request with a clear description of your changes.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🌟 Acknowledgments

- NASA for providing the incredible APOD API
- Apache Airflow community for the robust orchestration framework
- PostgreSQL for reliable data storage

---

_May your data pipelines be as infinite as the cosmos!_ ✨🪐
