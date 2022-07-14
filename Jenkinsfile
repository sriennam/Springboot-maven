pipeline {
    agent any
    tools {
       maven 'Maven'
    }
    environment {
        registry= '053518678618.dkr.ecr.eu-central-1.amazonaws.com/dockerfirstpipeline' 
        registryCredientials = 'jenkins-ecr-user'
        dockerimage = ''
    }
    stages {
         stage ('checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/sriennam/Springboot-maven.git']]])
            }
        }
        
       
        stage('Build') {
            steps {
                sh 'mvn clean package  -DskipTests'
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
                    docker.withRegistry('https://' + registry, 'ecr:eu-central-1:' + registryCredientials ) {
                    dockerImage.push()
                    }
                }      
            }          
        }
    }
        post {
        success {
            mail bcc: '', body: 'Pipeline build successfully', cc: '', from: 'srideviennam@gmail.com', replyTo: '', subject: 'The Pipeline success', to: 'srideviennam@gmail.com'
        }
        failure {  
            mail bcc: '', body: 'Pipeline build not success', cc: '', from: 'srideviennam@gmail.com', replyTo: '', subject: 'The Pipeline failed', to: 'srideviennam@gmail.com'
         } 
    }
        
//         stage('sonarqube checks') {
//             steps {
//                 script {
//                 withSonarQubeEnv(installationName: 'sonarqubecloud1', credentialsId: 'sonar-token-jenkin') {
//                  sh 'mvn clean package sonar:sonar'
//                  }
//                     timeout(time: 1, unit: 'HOURS') {
//                        def qg = waitForQualityGate()
//                     if (qg.status != 'OK') {
//                        error "Pipeline aborted due to quality gate failure: ${qg.status}"
//                         }
//                 }
//             }
//         }
//     }
//}
}
