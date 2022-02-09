pipeline {
    //agent any
    agent { docker { image 'maven:3.8.4' } }
    environment {
        dockerHome = tool 'myDocker'
        mavenHome = tool 'myMaven'
        PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
    }
    stages {
        stage('Build') {
            steps {
                echo "PATH - $PATH"
                sh 'mvn --version'
                sh 'docker version'
                echo "Build"
                echo "BUILD_NUMBER - $env.BUILD_NUMBER"
                echo "BUILD_ID - $env.BUILD_ID"
                echo "JOB_NAME - $env.JOB_NAME"
                echo "BUILD_TAG - $env.BUILD_TAG"
                echo "BUILD_URL - $env.BUILD_URL"
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