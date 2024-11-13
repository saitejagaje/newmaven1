pipeline
{
  agent any
  stages
  {
    stage('contdownload')
    {
      steps
      {
         git 'https://github.com/IntelliqDevops/maven.git'
      }
    }
  
   stage('contbuild')
        {
            steps
            {
               sh 'mvn package'
            }
        }
    stage('contdeploy')
         {
             steps
             {
                 deploy adapters: [tomcat9(credentialsId: 'new-credentials', path: '', url: 'http://172.31.3.150:8080')], contextPath: 'testapp3', war: '**/*.war'
             }
         }
         stage('conttesting')
            {
                steps
                {
                    git 'https://github.com/IntelliqDevops/FunctionalTesting.git'
                    sh 'java -jar /var/lib/jenkins/workspace/declaritivepipeline1/testing.jar'
                }
            }
            stage('condelivery')
            {
                steps
                {
                    deploy adapters: [tomcat9(credentialsId: 'new-credentials', path: '', url: 'http://172.31.11.79:8080')], contextPath: 'prodapp3', war: '**/*.war'
                }
            }
    }
}
