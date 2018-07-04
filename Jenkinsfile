pipeline {
    agent any
    
    /*
    parameters { 
         string(name: 'tomcat_dev', defaultValue: '18.217.54.10', description: 'Staging Server')
         string(name: 'tomcat_prod', defaultValue: '18.191.194.166', description: 'Production Server')
    }
    */
 
    triggers {
         pollSCM('* * * * *') // Polling Source Control
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
                        bat "C:\\Users\\WorkWork\\Desktop\\winscptoawstest.bat"
                    }
                }
 
                stage ("Deploy to Production"){
                    steps {
                        bat "C:\\Users\\WorkWork\\Desktop\\winscptoawsprod.bat"
                    }
                }
            }
        }
    }
}