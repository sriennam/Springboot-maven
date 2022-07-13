pipeline {
    agent any
    tools {
       maven 'maven 3.8.6'
    }
    environment {
        registry= '016003963452.dkr.ecr.us-east-1.amazonaws.com/dockerdemopipeline' 
        registryCredientials = 'jenkins-ecr-user'
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
        stage('Deploy the image to Amazon ECR') {
            steps {
                script {
                    docker.withRegistry('https://' + registry, 'ecr:us-east-1:' + registryCredientials ) {
                    dockerImage.push()
                    }
                }      
            }          
        }                 
    }
}
