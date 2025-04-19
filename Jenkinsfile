pipeline{
    agent any 
    tools{
        nodejs "node22"
    }

    stages{
        stage("Git Checkout"){
            steps{
                checkout scm
            }
        }

        stage("Test"){
            steps{
                sh "npm install"
                sh "npm test"
            }
        }

        stage("Build"){
            steps{
                sh "npm run build"
            }
        }
    }
}
