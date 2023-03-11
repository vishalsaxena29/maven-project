pipeline
{
  agent { label 'New-Agent1'}
  
  parameters {
    choice choices: ['dev', 'prod'], name: 'select_environment'
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
                agent { label 'New-Agent1'}
                steps{
                    echo "This is test stage A"
                    sh "mvn test"
                }
            }
            stage('testB')
            {
                agent { label 'New-Agent1'} 
                steps{
                    echo "This is test stage B"
                    sh "mvn test"
                }
            }
        }
        post {
        success {
            //archiveArtifacts artifacts: '**/target/*.war'
            dir("webapp/target/")
            {
                stash name: "maven-build", includes: "*.war"
            }
            }
        }
    }

    stage ('Deploy')
    {
        when {
            expression {
                params.select_environment == 'dev'
            }
            beforeAgent true
            agent { label 'New-Agent1'}
            steps {
                dir("/var/www/html")
                {
                    unstash maven-build
                }
                sh """
                cd /var/www/html
                jar -xvf webapp.war
                """
            }
        }
    }
  }
}