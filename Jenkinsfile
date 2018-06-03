pipeline {
   agent any
   tools {
    maven 'localMaven'
    }
    tools {
     jdk 'localJDK'
     }
   stages{
       stage('Init') { // for display purposes
          // Get some code from a GitHub repository
          steps{
          bat 'echo step1'
          }
          // Get the Maven tool.
          // ** NOTE: This 'M3' Maven tool must be configured
          // **       in the global configuration.
       }
       stage('Build') {
          // Run the maven build
          steps{
          bat 'mvn clean package'
          }
          post{
            success{
                bat 'echo Now Archiving..,'
                archiveArtifacts artifacts: '**/target/*.war'
            }
          }
       }
       stage('Deploy to staging') {
           steps{
          bat 'echo step3'
          build job: 'Deploy-to-sstaging'
           }
       }
       stage('Deploy to prod'){
            steps{
                timeout(time: 5, unit: 'DAYS'){
                    input message: "aaaaa"
                }
                build job: 'deploy-to-prod'
            }
            post {
                success {
                    echo "succcess deploy to prod"
                }
                failure {
                    echo 'fail deploy'
                }
            }
       }
   }
}
