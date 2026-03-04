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

stage('SonarQube Analysis') {
    steps {
        echo "Running SonarQube analysis"
        // 1. First, build the project to generate the target folder
        dir('sample-app') {
            sh 'mvn clean verify -DskipTests'
        }
        
        // 2. Then, run the scanner separately
        withSonarQubeEnv('SonarQube') {
            dir('sample-app') {
                sh 'mvn sonar:sonar -Dsonar.projectKey=webapp -Dsonar.projectName=webapp'
            }
        }
    }
}

    } // Closes stages
} // Closes pipeline
