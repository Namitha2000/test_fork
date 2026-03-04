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
        dir('sample-app') { 
            // 1. Run clean and verify first to generate the target folder
            sh 'mvn clean verify -DskipTests'
            
            // 2. FORCE: Re-create the directory and file after 'clean' has deleted them
            sh '''
            mkdir -p target/sonar
            touch target/sonar/report-task.txt
            chmod 777 target/sonar/report-task.txt
            '''
            
            // 3. Now run the Sonar scan
            withSonarQubeEnv('SonarQube') {
                sh 'mvn sonar:sonar -Dsonar.projectKey=webapp -Dsonar.projectName=webapp -Dsonar.working.directory=target/sonar'
            }
        }
    }
}    

    } // Closes stages
} // Closes pipeline
