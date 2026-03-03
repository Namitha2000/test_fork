pipeline {
    agent any

    tools {
        jdk 'jdk17'
        maven 'maven3'
    }

    parameters {   
        string(name: 'SONAR_IP', defaultValue: '13.50.246.94', description: 'IP of SonarQube server')
    }

    environment {
        SONARQUBE_URL = "http://${params.SONAR_IP}:9000"
        SONARQUBE_TOKEN = credentials('SonarQube') 
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'jenkinspv1',
                    url: 'https://github.com/Namitha2000/test_fork.git'
            }
        }

        stage('Build') {
            steps {
                dir('sample-app') {
                    sh 'mvn clean package -DskipTests'
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                dir('sample-app') {
                    sh """
                        mvn sonar:sonar \
                          -Dsonar.projectKey=sample-app \
                          -Dsonar.host.url=$SONARQUBE_URL \
                          -Dsonar.login=$SONARQUBE_TOKEN
                    """
                }
            }
        }
    }

    post {
        always {
            echo "Pipeline finished."
        }
    }
}
