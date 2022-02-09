pipeline {
    agent any
    //agent { docker { image 'maven:3.8.4' } }
    environment {
        dockerHome = tool 'myDocker'
        mavenHome = tool 'myMaven'
        PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
    }
    stages {
        stage('Checkout') {
            steps {
                echo "Checkout"
                sh 'mvn --version'
                sh 'docker version'
                echo "PATH - $PATH"
                echo "BUILD_NUMBER - $env.BUILD_NUMBER"
                echo "BUILD_ID - $env.BUILD_ID"
                echo "JOB_NAME - $env.JOB_NAME"
                echo "BUILD_TAG - $env.BUILD_TAG"
                echo "BUILD_URL - $env.BUILD_URL"
            }
        }
        stage('Compile') {
            steps {
                echo "Compile"
                sh 'mvn clean compile'
            }
        }
        stage('Test') {
            steps {
                echo "Test"
                sh "mvn test"
            }
        }
        stage('Integration Test') {
            steps {
                echo "Integration Test"
                sh "mvn failsafe:integration-test failsafe:verify"
            }
        }
        stage('Package') {
            steps {
                sh "mvn package -DskipTests"
            }
        }
        stage('Build Docker Image') {
            steps {
                echo "Build Docker Image"
                //"docker build -t markafirth/currency-exchange-devops:$env.BUILD_TAG"
                script {
                    dockerImage = docker.build("markafirth/currency-exchange-devops:${env.BUILD_TAG}")
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                echo "Push Docker Image"
                script {
                    docker.withRegistry('', 'dockerhub') {
                        dockerImage.push();
                        dockerImage.push('latest');
                    }
                }
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