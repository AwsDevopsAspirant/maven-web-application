node{
def mvn_home = tool name: "maven3.8.4"
stage('checkoutcode'){
git branch: 'development', credentialsId: 'aae8807e-4f9a-4055-bb65-f96c35956975', url: 'https://github.com/AwsDevopsAspirant/maven-web-application.git'
}
stage('Build'){
sh "${mvn_home}/bin/mvn clean package"
}
stage('ExcuteSonarQubeReport'){
sh "${mvn_home}/bin/mvn clean sonar:sonar"
}
stage('DeployIntoNexusArtificatory'){
sh "${mvn_home}/bin/mvn clean deploy"
}
stage('DeployIntoTomcat'){
sshagent(['d957c20d-4c81-405d-948b-16798b20acf3']) {
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.126.71.6:/opt/apache-tomcat-9.0.56/webapps/"
}
}
stage('EmailNotification'){
emailext body: '''Build Over..

Regards,
Awsdevops''', subject: 'Build Status', to: 'awsdevops.aspirant@gmail.com'
}
}
