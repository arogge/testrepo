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
  }
}
