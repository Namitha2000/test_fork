pipeline {
    agent any

    tools {
        jdk 'jdk17'
        maven 'maven3'
    }

    environment {
        SONAR_SERVER = 'SonarQube' // Name configured in Jenkins SonarQube plugin
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
                    withSonarQubeEnv('SonarQube') {
                        sh '''
                        mvn clean verify sonar:sonar \
                        -Dsonar.projectKey=sample \
                        -Dsonar.projectName=sample \
                        -Dsonar.host.url=$SONAR_HOST_URL \
                        -Dsonar.login=$SONAR_AUTH_TOKEN
                        '''
                    }
                }
            }
        }
    }
}
