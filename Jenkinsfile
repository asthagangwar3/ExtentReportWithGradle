pipeline {
    agent {label 'Jenkins Slave'}
	options {
        // This is required if you want to clean before build
        skipDefaultCheckout(true)
    }

    stages {
        stage ('Clean workspace') {
          steps {
                  cleanWs()
                }
	  }
	  stage ('Git Checkout') {
           steps {
                 checkout([$class: 'GitSCM', branches: [[name: '*']], extensions: [], 
			   userRemoteConfigs: [[url: 'https://github.com/asthagangwar3/ExtentReportWithGradle.git/']]])
                 }
	     }
	  stage ('gradle test')
	  {
	      steps {
	          sh 'gradle clean -i test'
	      }
	  }
	  
	  
    }
    post('Publish report') {
    always {
      script {
        publishHTML(target : [
          allowMissing         : false,
          alwaysLinkToLastBuild: true,
          keepAll              : true,
          reportDir            : 'test-output/',
          reportFiles          : 'ExtentReports.html',
          reportName           : 'Extent Report Demo'
        ])
      }
    }
  }
}
