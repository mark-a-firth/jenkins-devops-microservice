pipeline {
    // agent any
    agent { docker { image 'node:17.4' } }
    stages {
        stage('Build') {
            steps {
                sh 'mvn --version'
                echo "Build"
            }
        }
        stage('Test') {
            steps {
                echo "Test"
            }
        }
        stage('Integration Test') {
            steps {
                echo "Integration Test"
            }
        }
    }
    post {
        always {
            echo "I run always!"
        }
        success {
            echo "I run on successful completion."
        }
        failure {
            echo "I run on failure."
        }
    }
}