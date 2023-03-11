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
    
    stage ('test')
    {
        parallel {
            stage('testA')
            {
                steps{
                    echo "This is test stage A"
                }
            }
            stage('testB')
            {
                steps{
                    echo "This is test stage B"
                }
            }
        }
        post {
        success {
            archiveArtifacts artifacts: '**/target/*.war'
            }
        }
    }
  }
}