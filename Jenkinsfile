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
                // dir block must be OUTSIDE withSonarQubeEnv so Jenkins finds the report
                dir('sample-app') { 
                    withSonarQubeEnv('SonarQube') {
                        sh '''
                        mvn clean verify sonar:sonar \
                        -Dsonar.projectKey=webapp \
                        -Dsonar.projectName=webapp \
                        -Dsonar.working.directory=target/sonar
                        '''
                    }
                }
            }
        }
    } // Closes stages
} // Closes pipeline
