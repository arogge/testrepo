pipeline {
  options {
    skipDefaultCheckout true
    disableConcurrentBuilds()
  }
  agent none

  stages {
   stage("built-in") {
     agent { label "master" }
     steps {
       dir("sources") {
         checkout scm
       }
       script {
         dir("sources") {
           sh 'git show HEAD'
           sh 'git cat-file commit HEAD'
	 }
       }
     }
    }
   stage("docker") {
       agent {
          docker {
            label 'docker'
            image 'centos8'
            alwaysPull true
            registryUrl 'https://registry.bareos.com'
            registryCredentialsId 'jenkins_at_registry_bareos_com'
          }
        }
     steps {
       dir("sources") {
         checkout scm
       }
       script {
         dir("sources") {
           sh 'git show HEAD'
           sh 'git cat-file commit HEAD'
	 }
       }
     }
    }
  }
}
