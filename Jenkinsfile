pipeline {
    agent any
    tools {
       maven 'maven 3.8.6'
    }
    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
                echo 'hi'
            }
        }
        stage ('checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/devopscbabu/Springboot-maven.git']]])
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('sonarqube checks') {
            steps {
                script {
                withSonarQubeEnv('sonarqube-1') {
                 sh 'mvn sonar:sonar'
                
                    }
                }
            }
        }
    }
}
