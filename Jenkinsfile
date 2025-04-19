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
                    withDockerRegistry(toolName: 'docker', url: 'https://hub.docker.com/') {
                        sh "docker build -t express:latest ."
                        sh "docker tag express:latest ajjai007/express:latest"
                        sh "docker push ajjai007/express:latest"
                    
                    }
                }
            }
        }

        stage("Docker Run"){
            steps{
                script{
                    withDockerRegistry(toolName: 'docker', url: 'https://hub.docker.com/') {
                        sh "docker run -d --name express_app -p 3000:3000 ajjai007/express"
                    }
                }
            }

        }
    }
}
