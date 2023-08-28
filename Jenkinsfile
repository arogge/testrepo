pipeline {
  agent none
  stages {
    stage("Test") {
      agent { 
        docker {
	  label 'docker' 
	  image 'repobuild'
	  args '--volume /etc/passwd:/etc/passwd'
	  alwaysPull true
	  registryUrl 'https://registry.bareos.com'
	  registryCredentialsId 'jenkins_at_registry_bareos_com'
	}
      }
      steps {
        sshagent(credentials: ['ssh-key-hsm-server']) {
          sh '''
	    ssh-add -l
	    ssh -l jenkins -p 20022 -F /dev/null -oUserKnownHostsFile=$WORKSPACE/ssh_known_hosts 78.35.144.140 uname -a
	  '''
	}
      }
    }
  }
}
