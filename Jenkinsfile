pipeline{
    agent any

    tools{
        maven 'Maven 3.6.3'
        jdk 'jdk_16'
    }

    stages{
        stage('Build'){
            steps{
                echo 'Hello World'
                sh 'java --version'
                sh 'mvn --version'
                sh 'mvn clean compile'
            }
        }
        stage('Test'){
            steps{
                sh 'mvn test'
            }
        }
        stage('Packing to JAR'){
            steps{
                sh 'mvn package'
                sh 'docker --version'
            }
            post {
                success {
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
        stage('Create docker image'){
            steps{
                sh 'docker build -t jonasfredriksson/jenkinsdemo:1.1 .'
            }
        }
        stage('Push docker image to docker hub'){
            steps{
                sh 'cat ~/my_password.txt | docker login --username foo --password-stdin'
                sh 'docker login --username foo --password-stdin < ~/my_password'
                sh 'echo "$MY_PASSWORD" | docker login --username foo --password-stdin'
            }
        }
    }
}