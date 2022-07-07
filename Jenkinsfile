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
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/cbabu85/maven_project.git']]])
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('compile') {
            steps {
                echo 'Compile my job'
            }
        }
    }
}
