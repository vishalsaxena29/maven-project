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
           sh 'mvn clean package -DskipTests=true'
      }
      post {
      success {
        archiveArtifacts artifacts: '**/target/*.war'
            }
        }
    }
  }
}