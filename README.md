# Real-Time Data Cleaning Pipeline for Medical and Healthcare Data using SparkNLP, Spark-Streaming, and Kafka

## Project Overview
This project implements a **real-time data cleaning pipeline** for **medical and healthcare data**, using **Apache Spark**, **Kafka**, and **Spark NLP**. The pipeline ingests streaming data from Kafka, processes it using NLP techniques to extract meaningful insights, cleanses raw HTML medical articles, and stores the cleaned data in **Parquet** format for further analysis.

## Features
- **Real-time Data Ingestion**: Consumes streaming data from Kafka topics.
- **Data Processing with Spark NLP**:
  - Cleans HTML content to extract actual article text
  - Removes references and bibliography
  - Deduplicates articles
  - Segments text into paragraphs
  - Detects and redacts Personally Identifiable Information (PII)
- **Batch Processing and Storage**: Saves processed data in **Parquet format** for efficient retrieval.
- **Scalable Architecture**: Built using **Apache Spark**, making it suitable for large-scale processing.

## Project Structure
```bash
.
├── app.py                 # Entry point for running the pipeline
├── config.py              # Configuration settings for Kafka & Spark
├── data_ingestion.py      # Reads data from Kafka
├── data_processing.py     # Cleans & extracts data using Spark NLP
├── pipeline.py            # Orchestrates the end-to-end data pipeline
```

## Technologies Used
- **PySpark**
- **Spark NLP** (Text Processing & NER)
- **Apache Spark** (Structured Streaming)
- **Apache Kafka** (Streaming Data Source)
- **Parquet** (Data Storage)

## Data Processing Workflow
1. **Kafka Producer** sends raw HTML content of medical articles to a Kafka topic (`medical-articles`).
2. **Data Ingestion Module (`data_ingestion.py`)**:
   - Reads the Kafka stream.
   - Extracts relevant fields (URL, raw HTML content).
3. **Data Processing Module (`data_processing.py`)**:
   - **HTML Cleaning**: Strips HTML tags, preserving only the main article text.
   - **Duplicate Removal**: Ensures unique entries in the dataset.
   - **Text Segmentation**: Splits article text into meaningful paragraphs.
   - **PII Redaction (Bonus)**: Uses Named Entity Recognition (NER) to detect and remove sensitive information.
4. **Pipeline Module (`pipeline.py`)**:
   - Streams processed data into a Parquet file (`clean_medical_data.parquet`).

## Data Output Structure
The processed data is stored in Parquet format, following this schema:

```python
class ArticleMetadata:
    url: HttpUrl
    title: str

class Article:
    text: str
    paragraphs: List[str]
    metadata: ArticleMetadata
```

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
    KAFKA_TOPIC = "medical-articles"
    STORAGE_PATH = "./clean_medical_data.parquet"
```

## Start the Pipeline
```bash
python app.py
```

## Future Enhancements
- Support for additional NLP models (e.g., sentiment analysis, medical term extraction).
- Integration with a database for improved query performance.
- UI dashboard for real-time data flow monitoring.

---

This project ensures efficient processing of large-scale medical article datasets, making it useful for research, analytics, and structured data retrieval.

