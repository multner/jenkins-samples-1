// Powered by Infostretch 

timestamps {

node () {

	stage ('App-IC - Checkout') {
 	 checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'git-login', url: 'https://github.com/multner/jenkins-samples-1']]]) 
	}
	stage ('App-IC - Build') {
 			// Maven build step
	withMaven(maven: 'maven') { 
 			if(isUnix()) {
 				sh "mvn package " 
			} else { 
 				bat "mvn package " 
			} 
 		} 
	}
	stage ('App-IC - Post build actions') {

		stage ('APP-IC - Quality Analysis') {
	withMaven(maven: 'maven-3.5.4') { 
 			if(isUnix()) {
 				sh "mvn sonar:sonar" 
			} else { 
 				bat "mvn sonar:sonar" 
			} 
 		} 
}

		/*
Please note this is a direct conversion of post-build actions. 
It may not necessarily work/behave in the same way as post-build actions work.
A logic review is suggested.
*/
		// Mailer notification
		step([$class: 'Mailer', notifyEveryUnstableBuild: true, recipients: 'ekmekm33@gmail.com', sendToIndividuals: false])
 
	}
}
}
