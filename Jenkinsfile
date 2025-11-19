pipeline {
    agent any

    tools {
        maven 'MAVEN_HOME'
    }

    stages {

        stage('Build') {
            steps {
                bat 'mvn clean install'
            }
        }

        stage('SonarQube Scan') {
            steps {
                script {
                    def scannerHome = tool 'SonarScanner'
                }
                withSonarQubeEnv('SonarServer') {
                    bat """
                        "${tool('SonarScanner')}\\bin\\sonar-scanner.bat" ^
                          -Dsonar.projectKey=lab12 ^
                          -Dsonar.sources=. ^
                          -Dsonar.java.binaries=target
                    """
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
