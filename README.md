# Realtime Data Processing Pipeline using Spark NLP and Kafka

## Project Overview
This project implements a real-time data processing pipeline using **Apache Spark**, **Kafka**, and **Spark NLP**. The pipeline ingests streaming data from Kafka, processes it using NLP techniques to extract meaningful insights, and stores the cleaned data in **Parquet** format for further analysis.

## Features
- **Real-time Data Ingestion**: Consumes streaming data from Kafka topics.
- **Data Processing with Spark NLP**:
  - Cleans HTML content
  - Extracts metadata (titles, paragraphs)
  - Detects Named Entities (NER)
  - Redacts sensitive information (PII)
- **Batch Processing and Storage**: Saves processed data in **Parquet format** for later use.
- **Scalable Architecture**: Built using **Apache Spark**, making it suitable for large-scale processing.

## Project Structure
```
.
├── app.py                 # Entry point for running the pipeline
├── config.py              # Configuration settings for Kafka & Spark
├── data_ingestion.py      # Reads data from Kafka
├── data_processing.py     # Cleans & extracts data using Spark NLP
├── pipeline.py            # Orchestrates the end-to-end data pipeline
```

## Technologies Used
- **Apache Spark** (Structured Streaming)
- **Spark NLP** (Text Processing & NER)
- **Apache Kafka** (Streaming Data Source)
- **PySpark**
- **Parquet** (Data Storage)

## Setup & Installation
### 1. Clone the Repository
```bash
git clone <repository_url>
cd <repository_name>
```

### 2. Install Dependencies
Ensure you have Python installed and set up a virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows use `venv\Scripts\activate`
pip install -r requirements.txt
```

### 3. Run Kafka & Spark
Ensure you have **Kafka** and **Spark** running. If using Docker, you can set up a `docker-compose.yml` file to start the services.

## Configuration
Modify `config.py` to update settings like Kafka topics, Spark master URL, and storage paths.

Example:
```python
class Config:
    KAFKA_BOOTSTRAP_SERVERS = "kafka:9092"
    SPARK_MASTER_URL = "spark://spark-master:7077"
    KAFKA_TOPIC = "data-pipeline"
    STORAGE_PATH = "./clean_data.parquet"
```

## Start the Pipeline
```bash
python app.py
```

## How It Works
1. **Kafka Producer** sends raw HTML content to a Kafka topic (`data-pipeline`).
2. **Data Ingestion Module (`data_ingestion.py`)**:
   - Reads the Kafka stream.
   - Extracts relevant fields (URL, HTML content).
3. **Data Processing Module (`data_processing.py`)**:
   - Cleans HTML content.
   - Extracts metadata (titles, paragraphs).
   - Applies Named Entity Recognition (NER) for sensitive data detection.
   - Redacts PII.
4. **Pipeline Module (`pipeline.py`)**:
   - Streams processed data to a Parquet file (`clean_data.parquet`).

## Future Enhancements
- Support for additional NLP models (e.g., sentiment analysis).
- Integration with a database for better query performance.
- UI dashboard for monitoring real-time data flow.
