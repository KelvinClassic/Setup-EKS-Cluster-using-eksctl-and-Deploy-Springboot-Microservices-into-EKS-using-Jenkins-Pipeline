pipeline {

    agent any

    tools{
        maven "Maven3"
    }

    environment{
        registry = '404578764941.dkr.ecr.us-west-2.amazonaws.com/my-docker-repo'
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

        stage('Build image'){
            steps{
                script{
                    docker.build registry
                }
            }
        }

        stage('Push image into ECR'){
            steps{
                sh 'aws ecr get-login-password --region us-west-2 | docker login --username AWS --password-stdin 404578764941.dkr.ecr.us-west-2.amazonaws.com'
                sh 'docker push 404578764941.dkr.ecr.us-west-2.amazonaws.com/my-docker-repo:latest'
            }
        }
        
        stage('K8S Deploy'){
            steps{
                withKubeConfig(caCertificate: '', clusterName: '', contextName: '', credentialsId: 'k8s', namespace: '', restrictKubeConfigAccess: false, serverUrl: '') {
                sh 'kubectl apply -f  eks-deploy-k8s.yaml'
                }
            }
        }
    }
}