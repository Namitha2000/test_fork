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
            // 1. Build the WAR
            sh 'mvn clean verify -DskipTests'

            script {
                // 2. Inject Sonar Env and Run Scan
                withSonarQubeEnv('SonarQube') {
                    sh '''
                    mvn sonar:sonar \
                    -Dsonar.projectKey=webapp \
                    -Dsonar.projectName=webapp \
                    -Dsonar.working.directory=target/sonar \
                    -Dsonar.scanner.skipEmptyReport=true
                    '''
                }
            }
        }
    }
}    

    } // Closes stages
} // Closes pipeline
