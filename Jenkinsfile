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
                sh "docker build -t bangodi/hiring:0.0.3 ."
            }
        }
        stage('docker push') {
           
            steps {
             
                      sh "docker login -u bangodi -p 
                      sh "docker push bangodi/hiring:0.0.3"
                 
            }
        }
          stage('docker deploy') {
           
            steps {
                  sshagent(['docker-host']) {
                     
                }
                
              }
          }
     }
}
