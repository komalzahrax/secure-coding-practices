pipeline {
    agent any

    tools {
        maven 'MAVEN_HOME'
        sonarScanner 'SonarScanner'
    }

    environment {
        SONAR_PROJECT_KEY = 'my_project'
        SONAR_SERVER_URL = 'http://localhost:9000'
        SONAR_TOKEN = '<PASTE_YOUR_TOKEN_HERE>'
    }

    stages {

        stage('Build') {
            steps {
                bat "mvn clean install"
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarServer') {
                    bat """
                        sonar-scanner ^
                        -Dsonar.projectKey=${SONAR_PROJECT_KEY} ^
                        -Dsonar.sources=. ^
                        -Dsonar.host.url=${SONAR_SERVER_URL} ^
                        -Dsonar.login=${SONAR_TOKEN}
                    """
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 3, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }

    }

    post {
        always {
            echo "Pipeline Finished."
        }
    }
}
