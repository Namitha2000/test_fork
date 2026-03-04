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
                // Ensure we are working inside the project folder where pom.xml is located
                dir('sample-app') {
                    
                    // 1. Build the project and skip tests to save time
                    sh 'mvn clean verify -DskipTests'

                    script {
                        // 2. Inject SonarQube environment variables
                        // Note: Using 'SonarQube' to match your exact System Configuration name
                        withSonarQubeEnv('SonarQube') {
                            
                            // 3. Run SonarQube Scan using the stable plugin version 3.9.1.2184
                            // This bypasses the communication bug in the default 4.0.0 version
                            sh '''
                                mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.9.1.2184:sonar \
                                -Dsonar.projectKey=webapp \
                                -Dsonar.projectName=webapp \
                                -Dsonar.working.directory=target/sonar
                            '''
                        }
                    }
                }
            }
        }


    } // Closes stages
} // Closes pipeline
