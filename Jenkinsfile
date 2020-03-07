pipeline {
    agent any


    tools{
        maven 'local maven'
    }


    parameters{
        string(name: 'tomcat_dev', defaultValue: 'localhost', description: 'Staging Server')
        string(name: 'tomcat_prod', defaultValue: 'localhost', description: 'Production Server')
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
                    echo '开始存档...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }


     stage ('Deployments'){
            parallel{
                stage ('Deploy to Staging'){
                    steps {
                        cp **/target/*.war /usr/local/tomcat-staging/webapps
                    }
                }


                stage ("Deploy to Production"){
                    steps {
                        cp **/target/*.war /usr/local/tomcat-production/webapps
                    }
                }
            }
        }
    }
}
