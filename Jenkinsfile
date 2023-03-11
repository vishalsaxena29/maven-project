pipeline
{
  agent { label 'New-Agent1'}
  
  parameters {
    string defaultValue: 'saxena', name: 'LAST_NAME'
  }

  environment {
    NAME = "Vishal"
  }

  tools {
    maven 'mymaven'
  }

  stages {

    stage ('Build')
    { 
      steps{
           sh 'mvn clean package -DskipTests=true'
           echo "Hello $NAME ${params.LAST_NAME}"
      }
      post {
      success {
        archiveArtifacts artifacts: '**/target/*.war'
            }
        }
    }
  }
}