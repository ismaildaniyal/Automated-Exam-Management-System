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

## Implementation
### Data Collection
Collect data about the number of students from batches 19, 20, 21, 22, and 23 in each domain (computer science, artificial intelligence, business analytics, software engineering, and electrical engineering). Also, collect information on the capacity of each room.

### Data Preprocessing
Clean and preprocess the data to ensure it is suitable for the k-means clustering algorithm.

### K-Means Clustering
Use the k-means clustering algorithm to group students based on their domains and batch numbers. Use the number of students from each domain and batch as features for clustering. Determine the optimal number of clusters.

### Seating Plan Generation
Generate a seating plan for each room based on the clusters formed. Ensure that the capacity of each room is not exceeded and optimize seating arrangements.

### Faculty Allocation
Allocate faculty members to each room based on the clusters formed. Ensure that each room has at least one faculty member from each domain.

### Reporting
Generate a report summarizing the seating plan and faculty allocation for each exam.

## Evaluation Criteria
- Correct implementation and functionality of the k-means clustering algorithm.
- Accuracy and efficiency of the seating plan generation.
- Accuracy of faculty assignments based on domain expertise.
- Code quality.

## Contributing
Contributions are welcome! Please fork the repository and submit a pull request for any enhancements or bug fixes.

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contact
For any inquiries or feedback, please reach out to [ismaildaniyal](https://github.com/ismaildaniyal).

---

## Sample Code

Here is a sample code snippet to demonstrate the implementation of the k-means clustering and seating plan generation:

```python
import pandas as pd
from sklearn.cluster import KMeans
import numpy as np

# Sample data
students_data = pd.DataFrame({
    'batch': [19, 19, 20, 20, 21, 21, 22, 22],
    'domain': ['CS', 'AI', 'BA', 'SE', 'EE', 'CS', 'AI', 'BA'],
    'num_students': [300, 350, 400, 450, 320, 330, 340, 360]
})

room_data = pd.DataFrame({
    'room_id': [1, 2, 3, 4],
    'capacity': [35, 30, 25, 35]
})

# Data Preprocessing
student_features = students_data[['batch', 'domain', 'num_students']].copy()
student_features = pd.get_dummies(student_features, columns=['domain'])

# K-Means Clustering
kmeans = KMeans(n_clusters=4, random_state=42)
students_data['cluster'] = kmeans.fit_predict(student_features)

# Seating Plan Generation
seating_plan = {}
for cluster in students_data['cluster'].unique():
    cluster_data = students_data[students_data['cluster'] == cluster]
    room_capacity = room_data['capacity'].tolist()
    seating_plan[cluster] = []

    for _, student_group in cluster_data.iterrows():
        room_assigned = False
        for i, capacity in enumerate(room_capacity):
            if student_group['num_students'] <= capacity:
                seating_plan[cluster].append({'room_id': room_data.iloc[i]['room_id'], 'students': student_group['num_students']})
                room_capacity[i] -= student_group['num_students']
                room_assigned = True
                break
        if not room_assigned:
            print(f"Unable to assign room for cluster {cluster} with {student_group['num_students']} students")

# Faculty Allocation
faculty_data = pd.DataFrame({
    'faculty_id': [1, 2, 3, 4],
    'domain': ['CS', 'AI', 'BA', 'SE']
})

faculty_allocation = {}
for cluster in students_data['cluster'].unique():
    cluster_domains = students_data[students_data['cluster'] == cluster]['domain'].unique()
    faculty_allocation[cluster] = []
    for domain in cluster_domains:
        faculty_member = faculty_data[faculty_data['domain'] == domain].iloc[0]
        faculty_allocation[cluster].append(faculty_member['faculty_id'])

# Reporting
print("Seating Plan:")
for cluster, rooms in seating_plan.items():
    print(f"Cluster {cluster}:")
    for room in rooms:
        print(f"  Room {room['room_id']} - {room['students']} students")

print("\nFaculty Allocation:")
for cluster, faculties in faculty_allocation.items():
    print(f"Cluster {cluster}: Faculty IDs {faculties}")
