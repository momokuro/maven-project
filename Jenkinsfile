pipeline {
    agent any
    
    parameters {
         string(name: 'tomcat_dev', defaultValue: '54.199.225.97', description: 'Staging Server')
         string(name: 'tomcat_prod', defaultValue: '18.181.146.183', description: 'Production Server')
    }

    tools {
        maven 'localMaven'
    }

    triggers {
         pollSCM('* * * * *')
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

            stage ('Deployments'){
                parallel{
                    stage ('Deploy to Staging'){
                        steps {
                            sh "scp -i /Users/seigenmiyamoto/udemy/Lean\ jenkins\ from\ a\ DevOps\ Guru/maven-project/tomcat-demo.pem **/target/*.war ec2-user@${params.tomcat_dev}:/var/lib/tomcat7/webapps"
                        }
                    }

                    stage ("Deploy to Production"){
                        steps {
                            sh "scp -i /Users/seigenmiyamoto/udemy/Lean\ jenkins\ from\ a\ DevOps\ Guru/maven-project/tomcat-demo.pem **/target/*.war ec2-user@${params.tomcat_prod}:/var/lib/tomcat7/webapps"
                        }
                    }
                }
            }
        }
    }
}

