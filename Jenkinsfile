pipeline {
    agent any

    tools {
        // Assumes 'MAVEN_HOME' is a configured tool name in Jenkins
        maven 'MAVEN_HOME'
    }

    stages {

        stage('Build') {
            steps {
                // FIX: Navigate to the subdirectory containing the pom.xml
                dir('my-project-root') { 
                    bat 'mvn clean install'
                }
            }
        }

        stage('SonarQube Scan') {
            steps {
                script {
                    def scannerHome = tool 'SonarScanner'
                }
                
                // FIX: Run the Sonar scan from the project root so it finds the pom.xml and 'target'
                dir('my-project-root') {
                    withSonarQubeEnv('SonarServer') {
                        // Using a multiline bat command for readability and consistency
                        bat """
                            "${tool('SonarScanner')}\\bin\\sonar-scanner.bat" ^
                            -Dsonar.projectKey=lab12 ^
                            -Dsonar.sources=. ^
                            -Dsonar.java.binaries=target
                        """
                    }
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
