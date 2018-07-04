pipeline {
    agent any

    parameters {
         string(name: 'tomcat_dev', defaultValue: '18.217.54.10', description: 'Staging Server')
         string(name: 'tomcat_prod', defaultValue: '18.191.194.166', description: 'Production Server')
    }

    triggers {
         pollSCM('* * * * *')
     }

stages{
        stage('Build'){
            steps {
                bat 'mvn clean package'
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
                        bat 'echo -y | pscp -i C:\\Users\\WorkWork\\Desktop\\DevOps\\AWS\\Keys\\tomcat-demo.pem **/target/*.war ec2-user@${params.tomcat_dev}:/var/lib/tomcat7/webapps'
                    }
                }

                stage ("Deploy to Production"){
                    steps {
                        bat 'echo -y | pscp -i C:\\Users\\WorkWork\\Desktop\\DevOps\\AWS\\Keys\\tomcat-demo.pem **/target/*.war ec2-user@${params.tomcat_prod}:/var/lib/tomcat7/webapps'
                    }
                }
            }
        }
    }
}