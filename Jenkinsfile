pipeline {
  agent none
  stages {
    stage("Test") {
      agent { label 'docker' }
      steps {
        sh 'find . -ls'
      }
    }
  }
}
