pipeline {
  agent none
  stages {
    stage("Test") {
      agent { 
        docker {
	  label 'docker' 
	  image 'repobuild'
	  alwaysPull true
	  registryUrl 'https://registry.bareos.com'
	  registryCredentialsId 'jenkins_at_registry_bareos_com'
	}
      }
      steps {
        sh 'find . -ls'
      }
    }
  }
}
