pipeline{
    agent any
    
    stages{
        
        stage('maven build'){
            steps{
                sh"mvn clean package"
            }
        }
        stage('docker build'){
            steps{
                sh "docker build -t bangodi/gana:0.0.3 ."
            }
        }
        stage('docker push'){
            steps{
                withCredentials([string(credentialsId: 'Docker-hub', variable: 'hubpwd')]) {
                    sh "docker login -u bangodi -p ${hubpwd}"
                    sh "docker push bangodi/gana:0.0.3"
               }
            }
        }
        stage('docker deploy'){
            steps{
                sshagent(['docker-demo']) {
                    sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.85.209 docker run -d -p 8081:8080 --name lovely bangodi/gana:0.0.3"
                }
            }
        }
    }
}
