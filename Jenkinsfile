pipeline {
  agent any
  tools{
      jdk 'java8'
      maven 'maven3' 
  }
  stages {
    stage('build') {
      steps {
        echo "This is Build Stage"
        echo "doing maven package"
            sh label: '', script: 'mvn package checkstyle:checkstyle'
      }
      post{
          success{
              echo "Archive the artifact"
              archiveArtifacts '**/*.war'
              echo "Publish Junit Test"
              junit '**/target/surefire-reports/*.xml'  
              echo "Doing checkstyle"
              checkstyle canComputeNew: false, defaultEncoding: '', healthy: '', pattern: '', unHealthy: ''
          }
      }
     } 
    stage('Deploy_to_dev') {
      // continues deployment  
      steps {
        echo "This is Deploy to dev Stage"
        build 'deploy_dev'
      }
     } 
    stage('Deploy_to_Prod') {
      //continues delivery
      steps {
        echo "This is Deploy to Prod Stage"
        // timeout(time: 30, unit: 'SECONDS') {
        // input 'Do want to deploy it to Production ?'
       // }
       // build 'deploy_dev'
      }  
    }
   } 
}
