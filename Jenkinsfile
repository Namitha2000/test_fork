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

        dir('sample-app') {
            sh 'mvn clean verify'
        }

        withSonarQubeEnv('SonarQube') {
            dir('sample-app') {
                sh '''
                mvn org.sonarsource.scanner.maven:sonar-maven-plugin:4.0.0.4121:sonar \
                -Dsonar.projectKey=webapp \
                -Dsonar.projectName=webapp \
                -Dsonar.host.url=$SONAR_HOST_URL \
                -Dsonar.login=$SONAR_AUTH_TOKEN
                '''
            }
        }
    }
}

} //Closes stages
} // Closes pipeline
