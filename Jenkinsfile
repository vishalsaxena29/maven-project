pipeline
{
  agent { label 'New-Agent1'}
  
  tools {
    maven 'Maven 3.3.9' 
    jdk 'jdk8'
  }

  stages {

    stage ('Build')
    { 
      steps{
          sh 'mvc clean package'
      }
      post {
      success {
        archiveArtifacts artifacts: '**/target/*.war'
            }
        }
    }
  }
}