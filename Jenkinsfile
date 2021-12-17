pipeline {
  options {
    skipDefaultCheckout true
    disableConcurrentBuilds()
  }
  environment {
    GIT_AUTHOR_NAME = "Jenkins"
    GIT_COMMITTER_NAME = "Jenkins"
    GIT_AUTHOR_EMAIL = "jenkins@bareos.com"
    GIT_COMMITTER_EMAIL = "jenkins@bareos.com"
    GIT_AUTHOR_DATE = "Wed Feb 16 14:00 2037 +0100"
    GIT_COMITTER_DATE = "Wed Feb 16 14:00 2037 +0100"
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
