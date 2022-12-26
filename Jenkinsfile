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
                sh "docker build -t bangodi/hiring:0.0.2 ."
            }
        }
        stage('docker push') {
           
            steps {
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
                sh "docker build -t bangodi/hiring:0.0.2 ."
            }
        }
        stage('docker push') {
           
            steps {
                withCredentials([string(credentialsId: 'Docker-hub', variable: 'hubpwd')]) {
                       sh "docker login -u bangodi -p ${hubpwd}"
                        sh "docker push bangodi/hiring:0.0.2"
                       }
                     
                 }
            }
        }
        
     }
}

                     
       
