// Powered by Infostretch 

timestamps {

node () {

	stage ('App-IC - Checkout') {
 	 checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'git-login', url: 'https://github.com/Glennouche/jenkins-sample-1']]]) 
	}
	stage('App-IC - Quality Analysis') {
		withMaven(maven: 'maven') {
			if(isUnix()){
				sh "mvn sonar:sonar"
			} else {
				bat "mvn sonar:sonar"
			}
		}
	}
	
	stage ('App-IC - Build') {
 			// Maven build step
	withMaven(maven: 'maven') { 
 			if(isUnix()) {
 				sh "mvn clean package " 
			} else { 
 				bat "mvn clean package " 
			} 
 		} 
	}
	stage ('APP-IC - Deploy') {
	withMaven(maven: 'maven') { 
 			if(isUnix()) {
 				sh "mvn deploy" 
			} else { 
 				bat "mvn deploy" 
			} 
 		} 
	}
	stage ('App-IC - Post build actions') {
/*
Please note this is a direct conversion of post-build actions. 
It may not necessarily work/behave in the same way as post-build actions work.
A logic review is suggested.
*/
		// Mailer notification
		step([$class: 'Mailer', notifyEveryUnstableBuild: true, recipients: 'glenn.judeau@gmail.com', sendToIndividuals: false])
 
	}
}
}
