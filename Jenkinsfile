pipeline{
    agent any
    
    stages{
    
        stage('Maven Package and Nexus Deploy'){
            
        environment{
        
            PATH = "/opt/maven3/bin:$PATH"
        }
            steps{
                sh script: 'maven clean deploy'
            }
          }
          
          stage('Tomcat Dev'){
            steps{
               sshagent(['tomcat-new']) {
                   sh "ssh -o StrictHostKeyChecking=no target/car-rentals*.war ec2-user@172.31.43.28:/opt/tomcat8/webapps"
                   sh "ssh ec2-user@172.31.43.28 /usr/sbin/sevice tomcat stop"
                   sh "ssh ec2-user@172.31.43.28 /usr/sbin/sevice tomcat start"
                } 
            
            }
          
          }
      }
}
