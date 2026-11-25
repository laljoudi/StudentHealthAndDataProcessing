# Student Health Data Pipeline

A Data Engineering course project that takes one dataset of 1,000 student health and lifestyle records through the full journey of a data pipeline: relational storage, document storage, stream-style filtering, and an interactive dashboard.

## Why this project

A student's sleep, stress, and study load are closely tied to their health, but raw records do not show those patterns on their own. The goal was to store the data in a well-structured way and make it easy to spot students who may be at risk.

## The data

The dataset contains 1,000 student records. Each record includes age, gender, heart rate, blood pressure, stress level (from a biosensor and from self-reporting), physical activity, sleep quality, mood, weekly study and project hours, and an overall health risk level. The dataset was provided as part of the course.

## How it works

### 1. Relational database (SQLite)

The raw spreadsheet was normalized into five linked tables: `Students`, `Health_Metrics`, `Stress_Levels`, `Lifestyle`, and `Study_And_Project`. Using Python and SQLite, the pipeline creates the schema, loads the CSV, runs create, read, update, and delete operations, adds indexes on frequently searched fields such as mood and study hours, and answers analytical questions such as the five highest heart rates or which students report poor sleep.

### 2. Document database (TinyDB)

Part of the data (student details with study and project hours) is converted into JSON documents and stored in TinyDB. This shows how the same information can be modeled more flexibly, and supports quick queries such as counting students by risk level.

### 3. Stream processing (PySpark)

The dataset is read as a simulated live stream, and PySpark filters it in real time for three warning signs: systolic blood pressure of 130 or higher, biosensor stress above 7, and more than 40 study hours.

### 4. Dashboard (Streamlit)

A Streamlit dashboard brings the results of all three stages into one place, so the data can be explored and filtered without writing queries.

## Technologies

Python, SQLite (SQL), TinyDB, PySpark, Streamlit, Google Colab

## Repository contents

| File | Description |
|---|---|
| `DataEngProject_(1).ipynb` | The complete pipeline, from loading the data to the dashboard |
| `DEproject/DE_Project.pdf` | Project report with the ER diagram, normalization steps, and screenshots |
| `DEproject/student_health_data.csv` | The dataset |

## Running the project

Open the notebook in Google Colab, make sure `student_health_data.csv` is available in the session, and run the cells in order.

## What I learned

- How to design a normalized relational schema, and why indexing matters for query speed
- When structured SQL storage fits better than semi-structured NoSQL documents, and the other way around
- How to process data as a stream with PySpark
- How to connect every stage of a pipeline, from raw data to a dashboard someone can actually use
