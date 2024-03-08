pipeline{
    agent{
        label any
    }
    stages{
        stage("Build Docker Image") {
            steps{
                sh "echo 'Construção da Imagem"
            }
        }

        stage("Push Docker Image") {
            steps{
                sh "echo 'Envio da Imagem"
            }
        }
        
        stage("Deploy no Kubernetes") {
            steps{
                sh "echo 'Deploy no Kubernetes"
            }
        }
    }
}