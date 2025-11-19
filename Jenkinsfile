pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('SonarQube Scan') {
            steps {
                withSonarQubeEnv('SonarServer') {
                    bat """
                        "${tool('SonarScanner')}\\bin\\sonar-scanner.bat" ^
                          -Dsonar.projectKey=secure-coding ^
                          -Dsonar.sources=. ^
                          -Dsonar.inclusions=**/*.py,**/*.js,**/*.html
                    """
                }
            }
        }

        stage('Quality Gate') {
            steps {
                waitForQualityGate abortPipeline: true   // ⬅ FIXED
            }
        }
    }
}
