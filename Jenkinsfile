pipeline
{

agent {
  label 'New-Agent1'
}

parameters {
    choice choices: ['dev', 'prod'], name: 'select_environment'
}

environment{
    NAME = "vishal"
}
tools {
  maven 'mymaven'
}

stages{

    stage('build')
    {
        steps {
            script{
                file = load "script.groovy"
                file.hello()
            }
            sh 'mvn clean package -DskipTests=true'
           
        }

        

    }

    stage('test')
    { 
        parallel {
            stage('testA')
            {
                agent { label 'New-Agent1' }
                steps{
                    echo " This is test A"
                    sh "mvn test"
                }
                
            }
            stage('testB')
            {
                agent { label 'New-Agent1' }
                steps{
                echo "this is test B"
                sh "mvn test"
                }
            }
        }
        post {
        success {
             dir("webapp/target/")
            {
            stash name: "maven-build", includes: "*.war"
                 }
                 }
            }

    }

    stage('deploy_dev')
    {
        when { expression {params.select_environment == 'dev'}
        beforeAgent true}
        agent { label 'New-Agent1' }
        steps
        {
            dir("/var/www/html")
            {
                unstash "maven-build"
            }
            sh """
            cd /var/www/html/
            chmod 777 webapp.war
            jar -xvf webapp.war
            """
        }
    }
}

}