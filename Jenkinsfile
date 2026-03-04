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
        dir('sample-app') {
            // 1. Build the WAR file normally
            sh 'mvn clean verify -DskipTests'

            // 2. Use the dedicated Scanner Tool (Ensure 'sonar-scanner' is configured in Global Tool Configuration)
            withSonarQubeEnv('SonarQube') {
                def sonarqubeScanner = tool 'sonar-scanner' 
                sh "${sonarqubeScanner}/bin/sonar-scanner \
                    -Dsonar.projectKey=webapp \
                    -Dsonar.sources=. \
                    -Dsonar.java.binaries=target/classes"
            }
        }
    }
}

    } // Closes stages
} // Closes pipeline
