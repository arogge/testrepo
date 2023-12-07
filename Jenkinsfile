pipeline {
  agent none
  stages {
    stage("Test") {
      agent { 
        docker {
          label 'podman' 
          image 'devtools'
          alwaysPull true
          registryUrl 'https://registry.bareos.com'
          registryCredentialsId 'jenkins_at_registry_bareos_com'
	      }
      }
      environment {
				HOME = "/tmp/user-home"
      }
      steps {
        fileOperations([folderCreateOperation('/tmp/user-home')])
        sh 'uname -a'
        sh 'mkdir -p $HOME'
      }
    }
  }
}
