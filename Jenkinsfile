pipeline {
    agent any

    stages {
        stage('Maven Build') {
            steps {
                sh "mvn clean package"
            }
        }
        
        stage('docker build') {
          
            steps {
                sh "docker build -t bangodi/gani:0.0.3 ."
            }
        }
        stage('docker push') {
           
            steps {
                withCredentials([string(credentialsId: 'docker-hub', variable: 'hubpwd')]) {
                      sh "docker login -u bangodi -p ${hubpwd}"
                      sh "docker push bangodi/gani:0.0.3"
                 }
            }
        }
          stage('docker deploy') {
           
            steps {
                  sshagent(['docker-host']) {
                      sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.28.205 docker run -d -p 8084:8080 --name lovely bangodi/gani:0.0.3"
                }
                
              }
          }
     }
}
