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
       stage('deploy to prod'){
                steps{
               timeout(time:5, unit:'days'){
                   input message 'please approve deployment to prod'
                }
               build job: 'deploy-to-prod'
            }
                 post{
                       success{ echo 'deployed to prod successfull'}
                       failure{ echo 'failed to deploy tp prod'}

           }
       }

       }

        }
