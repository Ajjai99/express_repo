pipeline{
    agent any 
    tools{
        nodejs "node22"
    }

    stages{
        stage("Git Checkout"){
            steps{
                git branch: 'main', credentialsId: 'GitHub_Credential', url: 'https://github.com/Ajjai99/express_repo.git'
            }
        }

        stage("Install Dependencies"){
            steps{
                sh "npm install"
            }
        }

        stage("Build"){
            steps{
                sh "npm run build"
            }
        }

        stage("Docker Build and Push"){
            steps{
                script{
                    withDockerRegistry(credentialsId: 'docker_cred', toolName: 'docker') {
                        sh "docker build -t express:latest ."
                        sh "docker tag express:latest ajjai007/express:latest"
                        sh "docker push ajjai007/express:latest"
                    } 
                }
            }

        }
    }
}
