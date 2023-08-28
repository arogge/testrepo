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
      environment {
        P11_KIT_SERVER_ADDRESS = 'unix:path=/tmp/p11-kit.sock'
      }
      steps {
        sshagent(credentials: ['ssh-key-hsm-server']) {
          sh '''
	    ssh -l jenkins -p 20022 -F /dev/null -oUserKnownHostsFile=$WORKSPACE/ssh_known_hosts 78.35.144.140 -fN -L /tmp/p11-kit.sock:/run/user/1001/p11-kit/pkcs11

	    curl --location --output putty.exe https://the.earth.li/~sgtatham/putty/latest/w64/putty.exe

	    osslsigncode sign \
	      -pkcs11module /usr/lib64/pkcs11/p11-kit-client.so \
	      -pkcs11cert 'pkcs11:serial=DECC1202815;object=Certificate' \
	      -key 'pkcs11:serial=DECC1202815;object=Kaffee' \
	      -pass 654321 \
	      -in putty.exe \
	      -out putty-signed.exe

	    osslsigncode verify putty-signed.exe
	  '''
	}
      }
    }
  }
}
