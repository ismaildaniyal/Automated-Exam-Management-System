# Automated Exam Management System

## Overview
This project aims to design and implement an automated exam management system that efficiently manages the seating plan and faculty allocation for students in various domains and batches. The system leverages the k-means clustering technique to automate the seating plan and faculty allocation.

### Project Goals
1. Use k-means clustering to group students based on their domains of study.
2. Group students based on batch distribution and room capacities, ensuring maximum room utilization without exceeding limits.
3. Assign faculty members to each exam room based on their expertise in the corresponding domain of study.

## Features
- **Data Collection**: Gather data about the number of students from different batches and domains, as well as room capacities.
- **Data Preprocessing**: Clean and preprocess data to ensure suitability for the k-means clustering algorithm.
- **K-Means Clustering**: Group students based on their domains and batch numbers.
- **Seating Plan Generation**: Create a seating plan for each room based on the clusters formed.
- **Faculty Allocation**: Assign faculty members to each room based on their domain expertise.
- **Reporting**: Generate a report summarizing the seating plan and faculty allocation for each exam.

## Requirements
- Python 3.x
- Jupyter Notebook
- Required Python libraries: NumPy, Pandas, Scikit-learn

## Installation
1. Clone the repository:
    ```bash
    git clone https://github.com/ismaildaniyal/UnSupervised_Learning_Agent.git
    cd UnSupervised_Learning_Agent
    ```
2. Install the required libraries:
    ```bash
    pip install -r requirements.txt
    ```

## Usage
1. Launch Jupyter Notebook:
    ```bash
    jupyter notebook
    ```
2. Open the `Exam_Management_System.ipynb` notebook.
3. Follow the instructions in the notebook to run the system.

