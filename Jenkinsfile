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

        withSonarQubeEnv('SonarQube') {
            dir('sample-app') {
                sh '''
                mvn clean verify sonar:sonar \
                -Dsonar.projectKey=webapp \
                -Dsonar.projectName=webapp
                '''
            }
        }
    }
}    

} //Closes stages
} // Closes pipeline
