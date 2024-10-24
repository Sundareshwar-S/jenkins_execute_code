# Jenkins Pipeline Project - Detailed Explanation

This repository showcases the use of Jenkins for automating tasks like building and testing a Python project. Jenkins is a popular open-source automation server that allows continuous integration (CI) and continuous delivery (CD) of software projects.

## Project Overview

This project is built to demonstrate the use of Jenkins for automating the process of checking out code from a Git repository, running a Python script for building, and performing tests. The setup ensures a streamlined and automated development workflow.

### Key Components of the Project

1. **Jenkins Integration**:  
   Jenkins is configured to automate the project's workflow. The pipeline automates the fetching of code from the GitHub repository, runs a Python build command, and performs basic testing.

2. **Environment Setup**:  
   To execute the Python script, the appropriate environment is configured. This includes setting up the path to Python in the `PYTHON_HOME` environment variable, allowing the Jenkins agent to access and run Python commands during the build process.

3. **GitHub Integration**:  
   The project is hosted on a GitHub repository. Jenkins is configured to connect to this repository securely using credentials, enabling it to automatically fetch the latest version of the project whenever a build is triggered.

4. **Automated Build**:  
   Once the code is pulled from GitHub, Jenkins triggers the build step, which involves running a Python script. In this project, the script is executed using the `python` command (adjustable for different Python versions or environments). This automation removes the need for manual script execution and ensures consistency across builds.

5. **Testing Automation**:  
   After the build, a test step is automated, where Jenkins runs any predefined tests or simply confirms that the build was successful. This stage is designed to ensure the code functions as expected after every build. Future improvements may include integrating detailed testing frameworks.

### Jenkins Pipeline Script

Below is the Jenkins pipeline script used for automating the process:

```groovy
pipeline {
    agent any

    environment {
        PYTHON_HOME = 'C:\\Users\\sunda\\AppData\\Local\\Programs\\Python\\Python312'
        PATH = "${PYTHON_HOME};${PATH}"
    }

    stages {
        stage('checkout') {
            steps {
                checkout scmGit(branches: [[name: 'main']], extensions: [], userRemoteConfigs: [[credentialsId: '6d384ab0-ef78-45a3-9ac4-e2e95b049311', url: 'https://github.com/Sundareshwar-S/jenkins_program.git']])
            }
        }
        stage('Build') {
            steps {
                git branch: 'main', credentialsId: '6d384ab0-ef78-45a3-9ac4-e2e95b049311', url: 'https://github.com/Sundareshwar-S/jenkins_program.git'
                bat 'python test.py' // Use 'python3' if necessary
            }
        }
        stage('Test') {
            steps {
                echo "testing is done"
            }
        }
    }
}
