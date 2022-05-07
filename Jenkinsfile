node 
{
 def mavenHome = tool name:"maven 3.8.5"
stage('CheckoutCode')
{
git branch: 'development', credentialsId: 'a09fe1c5-0b4b-4bf3-96d5-833506fecc58', 
url: 'https://github.com/Krishna9678/maven-web-application.git'
}

stage('Build')
{
sh "${mavenHome}/bin/mvn clean package"
}

stage('ExecuteSonarQubeReport')
{
sh "${mavenHome}/bin/mvn clean sonar:sonar"
}

stage('UploadArtifactIntoNexus')
{
sh "${mavenHome}/bin/mvn clean deploy"
}

stage('DeployAppIntoTomcat')
{
sshagent(['eacebee0-9e03-444a-abf7-b301710768f1']) 
{
  sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.232.24.77:/opt/apache-tomcat-9.0.62/webapps/" 
}
stage('Send Notifications')
{
 emailext body: '''Build Over..

Regards,
Jyothi Technologies,
9959989678.''', subject: 'Build Over..', to: 'dhamma.krish@gmail.com'  
}
}
}
