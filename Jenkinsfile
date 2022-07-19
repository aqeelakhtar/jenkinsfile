pipeline
{
 agent any
 stages
 {
    stage("continuousdownload")
    {
         steps
         {
           git ' https://github.com/aqeelakhtar/maven.git'
         }
    }
    stage("continuousbuild")
    {
         steps
         {
           sh 'mvn package'
         }
    }
    stage("continuousdeployment")
    {
         steps
         {
           sh 'scp /var/lib/jenkins/workspace/declarativepipeline/webapp/target/webapp.war ubuntu@172.31.2.88:/var/lib/tomcat9/webapps/testapp.war'
         }
         
    }
    stage("continuoustesting")
    {
         steps
         {
           git 'https://github.com/aqeelakhtar/FunctionalTesting.git'
           sh 'java -jar /var/lib/jenkins/workspace/declarativepipeline/testing.jar'
         }
    }
    stage("continuousdelivery")
    {
         steps
         {
           input message: 'need approval frpm scrum master', submitter: 'aqeelar'   
           sh 'scp /var/lib/jenkins/workspace/declarativepipeline/webapp/target/webapp.war ubuntu@172.31.7.82:/var/lib/tomcat9/webapps/proapp.war'
         }
    }

  }
}
