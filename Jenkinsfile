pipeline {
    agent any
    tools{
        maven 'local maven'
    }
    stages{
        stage ('build'){
            steps{
                sh 'mvn clean package'
            }
        }
    }
}
