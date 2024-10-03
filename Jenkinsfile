pipeline {
    agent any
    tools{
        maven "Maven3"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/KelvinClassic/Setup-EKS-Cluster-using-eksctl-and-Deploy-Springboot-Microservices-into-EKS-using-Jenkins-Pipeline.git']])
            }
        }
        stage('Build Jar'){
            steps{
                sh 'mvn clean install'
            }
        }
    }
}