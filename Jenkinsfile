pipeline {
    agent any

    tools {
        jdk 'jdk17'
        maven 'maven3'
    }

    environment {
        SONAR_SERVER = 'SonarQube'
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo "Checking out source code"
                git url: 'https://github.com/Namitha2000/test_fork.git', branch: 'main'
            }
        }

        stage('Build & SonarQube Analysis') {
            steps {
                echo "Building and running SonarQube analysis"
                withSonarQubeEnv('SonarQube') {
                    dir('sample-app') {
                        // Combining clean, verify, and sonar:sonar in a single Maven command
                        sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=webapp -Dsonar.projectName=webapp'
                    }
                }
            }
        }
    } // Closes stages
} // Closes pipeline
