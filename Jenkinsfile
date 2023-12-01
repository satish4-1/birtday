pipeline{
    agent any
    
    environment{
        PATH = "/opt/maven3/bin:$PATH"
    }
    stages{
        stage("Git Checkout"){
            steps{
                git credentialsId: 'c8740120-86b3-41fa-932e-e432886f887b', url: 'https://github.com/satish4-1/birtday.git'
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
               sshagent(['admin'])  {
                sh "
                    scp -o StrictHostKeyChecking=no target/myweb.war  ubuntu@172.31.46.190:/home/ubuntu/var/www/html/                    
                                      
                                
                "
            }
            
            }
        }
    }
}
