pipeline {
    agent any

    tools {
        maven 'localMaven'
        docker 'localDocker'
    }

    stages{
        stage('Build'){
            steps{
                sh 'mvn clean package'
                sh "echo ${PATH}"
                sh "docker build . -t tomcatwebapp:${env.BUILD_ID}"
            }
        }
    }
}
