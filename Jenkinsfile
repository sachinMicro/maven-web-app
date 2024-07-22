pipeline{

    agent any

    tools{
        maven "Maven3.9.8"
    }

     stages{
        stage("Git Clone"){
            steps{
               git branch: "main" url: "https://github.com/sachinMicro/maven-web-app.git" 
            }
        }
        stage("Maven Build"){
            steps{
                sh "mvn clean package"
            }
        }
        stage("Deploy in Tomcat by SSH Agent"){
            steps{
                sshagent(['tomcat-server']) {
                 sh "scp -o StrictHostKeyChecking=no target/maven-web-app.war ec2-user@13.232.250.102:/home/ec2-user/apache-tomcat-9.0.91/webapps"
              } 
           }
        }
     }
}