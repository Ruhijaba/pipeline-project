node

{
def mavenHome = tool name: "maven 3.6.3"
stage('Checkoutcode')
{
git branch: 'development', credentialsId: '1f419a06-0403-42f4-a642-7b87614024c6', url: 'https://github.com/Ruhijaba/maven-web-application.git'
}
stage ('Build')
{
sh "${mavenHome}/bin/mvn clean package"
}
stage ('SonarQube Execute')
{
sh "${mavenHome}/bin/mvn sonar:sonar"
}
stage ('Uploadartifact in to nexus')
{
sh "${mavenHome}/bin/mvn deploy"
}
stage ('Deploy app into Tomcat')
{
sshagent(['a624fadd-b54e-42b4-92ac-845536e3b4cd']) 
{
sh "scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/pipeline-project/target/maven-web-application.war ec2-user@13.235.248.55:/opt/apache-tomcat-9.0.37/webapps/"}
}
stage('send email')
{
emailext body: '''Buid over

Regards
Roohi''', subject: 'Build is over', to: 'shanumpl21225@gmail.com,ruhijabaroo6@gmail.com'
} 
}
