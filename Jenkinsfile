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
                sh "docker build . -t bangodi/hiring:${commit_id()}"
            }
        }
        stage('docker push'){
            steps{
                withCredentials([string(credentialsId: 'Docker-hub', variable: 'hubpwd')]) {
                    sh "docker login -u bangodi -p ${hubpwd}"
                    sh "docker push bangodi/hiring:${commit_id()}"
               }
            }
        }
        stage('docker deploy'){
            steps{
                sshagent(['docker-demo']) {
                 sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.85.209 docker rm -f hiring"
                 sh "ssh ec2-user@172.31.85.209 docker run -d -p 8081:8080 --name hiring bangodi/hiring:${commit_id()}"
                }
            }
        }
    }
}

def commit_id(){
     sh returnStdout: true, script: 'git rev-parse HEAD'
    return id
}
