pipeline {
    agent any

    tools {
        maven 'MAVEN_HOME'
        sonarScanner 'SonarScanner'
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Sonar Scan') {
            steps {
                withSonarQubeEnv('SonarServer') {
                    sh '''
                        sonar-scanner \
                        -Dsonar.projectKey=lab12 \
                        -Dsonar.sources=. \
                        -Dsonar.java.binaries=target
                    '''
                }
            }
        }
    }
}
