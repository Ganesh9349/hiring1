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
                sh "docker build -t bangodi/hiring:0.0.2 ."
            }
        }
        stage('docker push'){
            steps{
                withCredentials([string(credentialsId: 'Docker-hub', variable: 'hubpwd')]) {
                    sh "docker login -u bangodi -p ${hubpwd}"
                    sh "docker push bangodi/hiring:0.0.2"
               }
            }
        }
        stage('docker deploy'){
            steps{
                sshagent(['docker-demo']) {
                    sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.85.209 docker run -d -p 8080:8080 --name hiring bangodi/hiring:0.0.2"
                }
            }
        }
    }
}
