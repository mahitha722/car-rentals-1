pipeline{
    agent any
     environment{
        
            
            TOMCAT_HOST = "ec2-user@172.31.43.28"
            TOMCAT_SVC = "/opt/tomcat8/bin/"
        }
    stages{
       
        stage('Maven Package and Nexus Deploy'){
            environment {
            PATH = "/opt/maven3/bin:$PATH"
           }
            steps{
                sh script: 'mvn clean deploy '
            }
          }
          
          stage('Tomcat Dev'){
            steps{
               sshagent(['tomcat-new']) {
                   sh "scp -o StrictHostKeyChecking=no target/car-rentals*.war ${TOMCAT_HOST}:/opt/tomcat8/webapps"
                   sh "ssh ${TOMCAT_HOST} ${TOMCAT_SVC}shutdown.sh"
                   sh "ssh ${TOMCAT_HOST} ${TOMCAT_SVC}startup.sh"
                } 
            
            }
          
          }
      }
    post {
  failure {
    // One or more steps need to be included within each condition's block.
     mail body: 'Hi Developer,Your job failed',
          subject: 'Job Failed',
          to: 'mahithabommu22@gmail.com'
  }
}
}
