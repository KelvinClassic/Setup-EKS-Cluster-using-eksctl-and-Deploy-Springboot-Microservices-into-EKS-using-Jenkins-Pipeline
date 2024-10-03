pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/KelvinClassic/Setup-EKS-Cluster-using-eksctl-and-Deploy-Springboot-Microservices-into-EKS-using-Jenkins-Pipeline.git']])
            }
        }
    }
}