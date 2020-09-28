//Steps:

//1.Install tomcat

//2.Go to /opt/tomcat

//3.Change permission to 777 web app “chmod 777 /tomcat/webapp” or

//4.Change the user owner  “sudo chown -R ubuntu:ubuntu tomcat/”

//5.Go to /opt/tomcat/bin

//6../ startup.sh

//7. In jenkin install sshagent plugin.

//8. Generate the pipleline syntax add, credentials username with private key.

//9. Add user name “ubuntu” and add private key “copy”

//10. Find below jenkins declarative file

pipeline{
  agent any
  stages{
    stage("Git Checkout"){
      steps{
            git credentialsId: 'github', url: 'https://github.com/aditya-malviya/myweb.git'
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
          sshagent(['tomcat-dev1']) {
          sh """
          scp -o StrictHostKeyChecking=no target/myweb.war  
          ubuntu@yourip:/opt/tomcat/webapps/
          ssh ubuntu@yourip /opt/tomcat/bin/shutdown.sh
          ssh ubuntu@yourip /opt/tomcat/bin/startup.sh
           """
            }
          }
        }
      }
    }
