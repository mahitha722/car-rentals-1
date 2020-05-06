pipeline{
    agent any
    
    stages{
    
        stage('Maven Package and Nexus Deploy'){
            
        environment{
        
            PATH = "/opt/maven3/bin:$PATH"
        }
            steps{
                sh script: 'mvn clean deploy'
            }
          }
          
          stage('Tomcat Dev'){
            steps{
               sshagent(['tomcat-new']) {
                   sh "scp -o StrictHostKeyChecking=no target/car-rentals*.war ec2-user@172.31.43.28:/opt/tomcat8/webapps"
                   sh "ssh ec2-user@172.31.43.28 /opt/tomcat8/bin/shutdown.sh"
                   sh "ssh ec2-user@172.31.43.28 /opt/tomcat8/bin/startup.sh"
                } 
            
            }
          
          }
      }
}
