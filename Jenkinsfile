node
{
def mavenHome = tool name:"maven3.8.1"
//properties([[$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('* * * * *')])])
properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('* * * * *')])])

stage ('checkoutscmcode')
{
git branch: 'development', credentialsId: '0ad58830-f0fb-48ca-be9e-3f8ff0210501', url: 'https://github.com/hafeezasifdevops/maven-web-application.git'
}

stage ('Build')
{
sh "${mavenHome}/bin/mvn clean package"
}
/*
stage	('SonarQubeReport')
{
sh "${mavenHome}/bin/mvn clean sonar:sonar"
}

stage	('NexusArtifactupload')
{
sh "${mavenHome}/bin/mvn deploy"
}

stage	('DeployAppinTomcatserver')
sshagent(['40177ad2-26ee-49c7-ae2c-5a969b67bdb3']) {
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.6.86.146:/opt/apache-tomcat-9.0.45/webapps"
}
*/
stage	('Email')
{
emailext body: '''Build Completed

Warm Regards,
AVRS''', subject: 'Build Completed', to: 'hafeez.asif.49@gmail.com'
}
}
