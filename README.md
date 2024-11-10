Data Download Duplication Alert System (DDAS)
Overview
The Data Download Duplication Alert System (DDAS) is a real-time AI-powered tool that prevents duplicate data downloads in multi-user environments like academic institutions or research labs. DDAS helps conserve storage and bandwidth while enhancing data management and reducing redundancy across networks.

Key Features
AI-Powered Duplicate Detection: Combines BERT (text), CNN (image), SimHash, and FAISS to detect similar files accurately.
Real-Time Alerts: WebSocket integration sends immediate notifications to users about potential duplicate files.
Resource Optimization: Reduces unnecessary downloads, saving bandwidth and storage.
Role-Based Access Control (RBAC): Ensures secure access based on user roles.
Audit Logging: Logs actions for transparency, security, and easy auditing.
Technology Stack
Backend: Java
Database: MySQL for metadata storage
AI Models: BERT for text similarity, CNN for image comparison, SimHash for hashing, FAISS for vector similarity search
Real-Time Alerts: WebSocket
Security: Role-Based Access Control (RBAC) for managing file permissions
Getting Started
Prerequisites
Java (version 11+)
MySQL (for metadata and log storage)
AI Libraries: Deeplearning4j, TensorFlow Java, and FAISS
WebSocket Libraries for Java
Installation
Clone Repository


https://github.com/Aman-1610/DDAS.git

Database Setup
Create a MySQL database (e.g., ddas_db) and configure credentials in config.properties.
Install Dependencies
Use Maven or Gradle to install Deeplearning4j, TensorFlow, FAISS, and WebSocket libraries.
Run Application

java -jar DDAS.jar

Usage Workflow
User Download Request: When a user requests a download, metadata is captured.
AI-Powered Duplicate Detection: The system analyzes the content with AI models:
Text: BERT
Image: CNN
Approximate Matching: SimHash and FAISS
Real-Time Notification: If a duplicate is found, users receive an alert with details.
Logging and Access Control: The system verifies permissions via RBAC and logs user actions.
System Architecture
User Initiates Request: User download request triggers metadata capture.
AI Model Processing: Text and images are processed through BERT, CNN, and SimHash.
Duplicate Detection: FAISS rapidly searches for duplicate vectors in the database.
Notification: WebSocket sends real-time duplicate alerts.
Logging: All interactions are recorded in the database for transparency.
Contributions
Contributions are welcome! Fork the repo, create a new branch, and submit a pull request.

License
This project is licensed under the MIT License. See the LICENSE file for details.
