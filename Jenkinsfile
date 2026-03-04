pipeline {
    agent any

    tools {
        jdk 'jdk17'
        maven 'maven3'
    }

    environment {
        SONAR_SERVER = 'SonarQube' // Name in Jenkins -> Configure System -> SonarQube servers
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Checking out source code"
                git url: 'https://github.com/Namitha2000/test_fork.git', branch: 'main'
            }
        }

        stage('Build & Sonar Analysis') {
            steps {
                echo "Building project and running SonarQube analysis"
                dir('sample-app') {
                    withSonarQubeEnv('SonarQube') {
                        sh '''
                        mvn clean verify sonar:sonar \
                          -Dsonar.projectKey=sample \
                          -Dsonar.projectName=sample \
                          -Dsonar.host.url=$SONAR_HOST_URL \
                          -Dsonar.token=$SONAR_AUTH_TOKEN
                        '''
                    }
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }

    post {
        always {
            echo "Cleaning workspace"
            cleanWs()
        }
        success {
            echo "Build and SonarQube analysis completed successfully!"
        }
        failure {
            echo "Build failed! Check SonarQube for details."
        }
    }
}
