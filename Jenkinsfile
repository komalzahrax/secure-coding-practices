pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                echo 'Checking out code...'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
            }
        }

        stage('Static Code Analysis (SAST)') {
            steps {
                echo 'Running SAST scan (simulated)...'
            }
        }

        stage('Dependency Check') {
            steps {
                echo 'Running dependency check (simulated)...'
            }
        }

        stage('Container Security Scan') {
            steps {
                echo 'Running container scan (simulated)...'
            }
        }

        stage('Unit Tests') {
            steps {
                echo 'Running unit tests...'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment...'
            }
        }

        stage('Security Gate') {
            steps {
                echo 'Checking security gate (simulated)...'
            }
        }

        stage('Deploy to Production') {
            when {
                branch 'main'
            }
            steps {
                echo 'Deploying to production (main branch)...'
            }
        }
    }

    post {
        always {
            echo 'Archiving security reports (simulated)...'
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
