pipeline {
    agent any
    
    tools {
        maven 'maven'
    }
    parameters {
         string(name: 'staging_server', defaultValue: '10.0.4.115', description: 'Remote Staging Server')
    }

stages{
        stage('Build'){
            steps {
              //  sh 'mvn clean package'
                  powershell ' \'mvn clean package\''                
            }
            post {
                success {
                    echo 'Archiving the artifacts'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deployments'){
            parallel{
                stage ("Deploy to Staging"){
                    steps {
                    //  sh "scp -v -o StrictHostKeyChecking=no **/*.war root@${params.staging_server}:/opt/tomcat/webapps/"
                        powershell 'copy StrictHostKeyChecking=no **/*.war root@${params.staging_server}:D:\\Gen\\Tom\\tom_test\\webapps\\'
                    }
                }
            }
        }
    }
}
