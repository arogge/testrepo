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
        sshagent(credentials: ['ssh-key-hsm-server']) {
          sh '''
	    ssh-add -l
	    [ -d ~/.ssh ] || mkdir ~/.ssh && chmod 0700 ~/.ssh
	    ssh-keyscan -p 20022 78.35.144.140 >> ~/.ssh/known_hosts
	    ssh -l jenkins -p 20022 78.35.144.140 uname -a
	  '''
	}
      }
    }
  }
}
