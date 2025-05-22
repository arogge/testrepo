pipeline {
  agent none
  stages {
    stage("Test") {
      node('testing-vm') {
        checkout scm
        steps {
          sh 'cmake -S . -B build'
          sh 'cd build && ctest -V -S CTestScript.cmake --output-on-failure'
        }
        archiveArtifacts artifacts: "build/**"
      }
    }
  }
}
