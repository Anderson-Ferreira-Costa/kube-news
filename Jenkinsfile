pipeline {
    agent any 

    stages {
        stage("Build Docker Image") {
            steps{
                script {
                    dockerapp = docker.build("andersonbatistaferreiracosta/kube-news:v${env.BUILD_ID}", '-f ./src/Dockerfile ./src' )
                }
            }
        }
        stage("Push Docker Image") {
            steps{
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        dockerapp.push("latest")
                        dockerapp.push("v${env.BUILD_ID}")
                    }
                }
            }
        }
        
        stage("Deploy no Kubernetes") {
            environment {
                tag_version = "${env.BUILD_ID}"
            }
            steps{
                // witchKubeConfig([credentialsId: 'kubeconfig']) {
                    sh 'sed -i "s/{{TAG}}/$tag_version/g" ./k8s/deployment.yaml'
                    sh 'kubectl apply -f k8s/deployment.yaml'
                // }
            }
        }
    }
}