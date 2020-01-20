pipeline {
    agent any
        stages {
            stage('package'){
                steps{

                    bat 'mvn clean package'
                }
                post{
                    success{
                        echo 'now archiving'
                        archiveArtifacts artifacts: '**/target/*.war'
                        

                    }
                }
            }
            stage('deploy to staging'){
                steps{
                    build job: 'deploy-to-staging'
                }
            }
        } 
}
