pipeline
{
  agent { label 'New-Agent1'}
  
  tools {
    maven 'mymaven'
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