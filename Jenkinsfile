// Version from Bash2 – Komal Zahra (22i-1613)
>>>>>>> 5c2c443219c7dd101dc38a8cafc7a709ef529a70
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
