pipeline {
    agent any

    tools {
        maven 'localMaven'
    }

    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('Deploy to Staging'){
            steps {
                build job: 'deploy-to-staging'
            }
        }

        stage('Deploy to Production'){
            steps {
                build job: 'deploy-to-prod'
            }
            post {
                success {
                    echo 'code deployed to Production'
                }
                
                failure {
                    echo 'Deployment failed.'
                }
            }
        }
    }
}

