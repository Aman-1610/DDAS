# Data Download Duplication Alert System (DDAS) Overview
The **Data Download Duplication Alert System (DDAS)** is an AI-driven tool designed to prevent duplicate downloads in multi-user environments, conserving storage and bandwidth while improving data management.

## Key Features
- **AI-Powered Duplicate Detection**: Utilizes BERT (text), CNN (images), SimHash, and FAISS for accurate duplicate detection.
- **Real-Time Alerts**: WebSocket integration provides instant notifications for potential duplicates.
- **Resource Optimization**: Reduces redundant downloads to save resources.
- **Role-Based Access Control (RBAC)**: Controls access based on user roles.
- **Audit Logging**: Records actions for security and transparency.

## Technology Stack
- **Backend**: Java
- **Database**: MySQL (metadata storage)
- **AI Models**: BERT, CNN, SimHash, FAISS
- **Real-Time Alerts**: WebSocket
- **Security**: RBAC for permissions

## Getting Started
### Prerequisites
- Java (11+)
- MySQL
- AI Libraries: Deeplearning4j, TensorFlow Java, FAISS
- WebSocket Libraries for Java

### Installation
1. **Clone Repository**: [GitHub Link](https://github.com/Aman-1610/DDAS.git)
2. **Database Setup**: Create a MySQL database (e.g., `ddas_db`) and configure credentials in `config.properties`.
3. **Install Dependencies**: Use Maven or Gradle to install necessary libraries.

### Run Application
```bash
java -jar DDAS.jar
```
## Usage Workflow
1. **User Download Request**: Captures metadata when a user initiates a download.
2. **AI-Powered Duplicate Detection**: Uses AI models to analyze content:
   - **Text**: BERT
   - **Image**: CNN
   - **Approximate Matching**: SimHash and FAISS
3. **Real-Time Notification**: Alerts user if a duplicate is found.
4. **Logging and Access Control**: RBAC verifies permissions and logs actions.

## System Architecture
1. **User Request**: Triggers metadata capture.
2. **AI Model Processing**: BERT, CNN, and SimHash process text and images.
3. **Duplicate Detection**: FAISS searches for duplicate vectors.
4. **Notification**: WebSocket sends real-time alerts.
5. **Logging**: Records all interactions in the database.

## Contributions
Contributions are welcome! Fork the repository, create a branch, and submit a pull request.

## License
This project is licensed under the **MIT License**. See the LICENSE file for details.
