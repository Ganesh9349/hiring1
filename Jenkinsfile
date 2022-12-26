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
                sh "docker login -u bangodi -p ******"
            }
        }
    }
}
