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
            // 1. Build first
            sh 'mvn clean verify -DskipTests'
            
            withSonarQubeEnv('SonarQube') {
                // 2. FORCE: Create the file right before the scan starts
                sh '''
                mkdir -p target/sonar
                echo "projectKey=webapp" > target/sonar/report-task.txt
                chmod 777 target/sonar/report-task.txt
                '''
                
                // 3. Run scan with absolute paths
                sh '''
                mvn sonar:sonar \
                -Dsonar.projectKey=webapp \
                -Dsonar.projectName=webapp \
                -Dsonar.working.directory=target/sonar \
                -Dsonar.scm.provider=git
                '''
            }
        }
    }
}



    } // Closes stages
} // Closes pipeline
