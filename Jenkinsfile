pipeline {
    agent any
    tools {
       maven 'Maven'
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
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/devopscbabu/Springboot-maven.git']]])
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package  -DskipTests'
            }
        }
        stage('sonarqube checks') {
            steps {
                script {
                withSonarQubeEnv(installationName: 'sonarqubecloud1', credentialsId: 'sonar-token-jenkin') {
                 sh 'mvn clean package sonar:sonar'
                 }
                    timeout(time: 1, unit: 'HOURS') {
                       def qg = waitForQualityGate()
                    if (qg.status != 'OK') {
                       error "Pipeline aborted due to quality gate failure: ${qg.status}"
                        }
                }
            }
        }
    }
}
}
