node{
	stage('SCM Checkout'){
		git branch: 'wartomcat', url: 'https://github.com/arunsunuwar/devopsprojects.git'
	}
	stage('Compile-Package'){
		def mvnHome = tool name: 'maven-3.5.4', type: 'maven'
		sh "${mvnHome}/bin/mvn package"
	}
	stage('Deploy to Tomcat'){
		sshagent(['tomcat-dev']) {
		sh 'scp -o StrictHostKeyChecking=no target/*.war ec2-user@107.22.122.86:/opt/tomcat9/webapps/'
	}
	}

stage('Slack Notification'){
	slackSend  baseUrl: 'https://hooks.slack.com/services/', channel: '#jenkinsnotification', color: '#439FE0', message: 'New Build deployed Arun', teamDomain: 'intelycoreworkspace', tokenCredentialId: 'slack-secret'
	}
  
	stage('Email Notification'){
	mail bcc: '', body: 'Built done', cc: '', from: 'achieverarun10@gmail.com', replyTo: '', subject: 'Build by Arun', to: 'achieverarun10@gmail.com'
	}
}
