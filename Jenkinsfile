pipeline{
    agent any
    
    environment{
        PATH = "/opt/maven3/bin:$PATH"
    }
    stages{
        stage("Git Checkout"){
            steps{
                git credentialsId: 'javahome2', url: 'https://github.com/satish4-1/birtday.git'
            }
        }
        stage("Maven Build"){
            steps{
                sh "mvn clean package"
                sh "mv target/*.war target/myweb.war"
            }
        }
        stage("deploy-dev"){
            steps{
                sshagent(['tomcat-new']) {
                sh """
                    scp -o StrictHostKeyChecking=no target/myweb.war  ubuntu@172.31.46.190:/home/ec2-user/apache-tomcat-9.0.64/webapps/
                    
                    ssh ubuntu@172.31.46.190 /home/ec2-user/apache-tomcat-9.0.64/bin/shutdown.sh
                    
                    ssh ubuntu@172.31.46.190 /home/ec2-user/apache-tomcat-9.0.64/bin/startup.sh
                
                """
            }
            
            }
        }
    }
}
