pipeline {
    agent any
    tools {
       maven 'maven 3.8.6'
    }
    environment {
         dockerimage = ''
    }
    stages {
       stage ('checkout') {
           steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/devopscbabu/Springboot-maven.git']]])
            }
        }
        stage('Build') {
            steps {
                sh 'mvn package'
            }
        }
        stage('Building the Image') {
        steps {
            script {
            dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
    }
    }
    }
}
