pipeline {
    agent any

    tools {
        maven 'MAVEN_HOME'
        sonarRunner 'SonarScanner'
    }

    stages {

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('SonarQube Scan') {
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

        stage('Quality Gate') {
            steps {
                timeout(time: 1, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
