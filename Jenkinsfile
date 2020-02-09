pipeline {
  agent {
    node {
      label 'master'
    }

  }
  options { disableConcurrentBuilds()
	  buildDiscarder(logRotator(numToKeepStr: '5', daysToKeepStr: '5'))}
   parameters 
   {
       string(name: 'BuildNo', defaultValue: '1.0.9.$BUILD_NUMBER', description: 'Build Number')
   }
   
   stages {
	   stage("Set Build Name"){
     steps {
        script {
            currentBuild.displayName = "${BuildNo}"
                }
           }
    }
  }
  post {
   success{
   	//Collecting the required artifacts.
	//archiveArtifacts 'DIPWebCtrlAddonService_Spring/target/**/*.*'
	//Send the email for build status.
   	emailext attachLog: true, body: '$DEFAULT_CONTENT', recipientProviders: [developers(), requestor()], replyTo: '$DEFAULT_REPLYTO', subject: '$DEFAULT_SUBJECT', to: '$BSP_Platform'
   }
   failure {
   	//Send the email for build status.
        emailext attachLog: true, body: '$DEFAULT_CONTENT', recipientProviders: [developers(), requestor()], replyTo: '$DEFAULT_REPLYTO', subject: '$DEFAULT_SUBJECT', to: '$BSP_Platform'
    }
    }
}


