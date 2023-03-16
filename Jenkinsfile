pipeline { 
  agent none 
  parameters { string(name: 'jfrog_user', defaultValue: '', description: ' this is user name for jfrog') 
               string(name: 'jfrog_pass', defaultValue: '', description: ' this is password for jfrog') } 
 environment { 
               MVN_HOME = "/home/rocky/apache-maven-3.9.0" 
 
             } 
 
 stages { 
 
   stage('build code and push code to artifact repo ') { 
     agent { label 'devops' } 
     steps { 
       sh "export PATH=$PATH:${env.MVN_HOME}/bin && mvn clean deploy" 
     } 
   } 
 
   stage('deployment on tomcat') { 
     agent { label 'tomcat-deploy' } 
     steps { 
       sh """ 
            wget --http-user=${jfrog_user} --http-password=${jfrog_pass} https://devops400.jfrog.io/artifactory/devops/com/mycompany/app/my-app-kingston/2.0/my-app-kingston-2.0.war
            mv my-app-kingston-2.0.war my-app-kingston.war 
            cp my-app-kingston.war /home/rocky/tomcat/tomcat9/webapps/ 
         """ 
     } 
   } 
 } 
 }
