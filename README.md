# STEDI Data Lakehouse

## Project Overview

The STEDI Team has been hard at work developing a hardware `STEDI Step Trainer`. This is a motion sensor that records the distance of the object detected. The app uses a mobile phone accelerometer to detect motion in the X, Y, and Z directions. The STEDI team wants to use the motion sensor data to train a machine learning model to detect steps accurately in real-time. Privacy will be a primary consideration in deciding what data can be used.

In this project, I will act as a data engineer to build a data lakehouse solution for sensor data that trains a machine learning model for the STEDI team. The data produced by the sensors and the mobile app will be extacted and curated them into a data lakehouse on AWS so that Data Scientists can train the learning model.

## Project Data

STEDI has three JSON data sources(opens in a new tab) to use from the Step Trainer. Check out the JSON data in the following folders in the Github repo:
- customer
- step_trainer
- accelerometer

## Project Repository

**Glue Jobs - Python files generated by AWS Glue Studio** 

- **customer_trusted.py** A Python script using Spark that sanitizes the Customer data from the Website (Landing Zone) and only store the Customer Records who agreed to share their data for research purposes (Trusted Zone). 
- **accelerometer_trusted.py** A Python script using Spark that sanitizes the Accelerometer data from the Mobile App (Landing Zone) - and only store Accelerometer Readings from customers who agreed to share their data for research purposes (Trusted Zone).
- **customer_curated.py** A Python script using Spark that sanitizes the Customer data (Trusted Zone) and create a Glue Table (Curated Zone) that only includes customers who have accelerometer data and have agreed to share their data for research.
- **step_trainer_trusted.py** A Python script using Spark that read the Step Trainer IoT data stream (S3) and populate a Trusted Zone Glue Table called step_trainer_trusted that contains the Step Trainer Records data for customers who have accelerometer data and have agreed to share their data for research.
- **machine_learning_curated.py** A Python script using Spark that creates an aggregated table that has each of the Step Trainer Readings, and the associated accelerometer reading data for the same timestamp, but only for customers who have agreed to share their data.

**Glue table (DDL)**
- **customer_landing.sql** SQL queries for creating a Glue table for (S3) customer landing zone.
- **accelerometer_landing.sql** SQL queries for creating a Glue table for (S3) accelerometer landing zone.

**Query Screenshots - AWS Athena**
- **customer_landing.png** A screenshot of Athena query customer_landing table.
- **customer_trusted.png** A screenshot of Athena query customer_trusted table. The output only contains Customer Records from people who agreed to share their data.
- **accelerometer_landing.png** A screenshot of Athena query accelerometer_landing table.
