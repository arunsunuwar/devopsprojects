node{
	stage('SCM Checkout'){
		git branch: 'wartomcat', url: 'https://github.com/arunsunuwar/devopsprojects.git'
	}
	stage('Compile-Package'){
		def mvnHome = tool name: 'maven-3.5.4', type: 'maven'
		sh "${mvnHome}/bin/mvn package"
	}
	stage('Deploy to Tomcat'){
		slackSend channel: '#jenkinsnotification', color: '#439f30', message: 'New Build Deploy test', teamDomain: 'intelycoreworkspace', tokenCredentialId: 'slack-secret' {
		sh 'scp -o StrictHostKeyChecking=no target/*.war ec2-user@http://107.22.122.86:/opt/tomcat9/webapps/'
	}
	}
}
