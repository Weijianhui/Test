pipeline {
  agent none
  stages {
    stage('master') {
      agent {
        node {
          label 'master'
          customWorkspace 'e:/jenkins'
        }

      }
      steps {
        powershell 'echo "ha"'
        echo 'OK'
      }
    }

  }
  post {
    success {
      echo 'success'
    }

  }
}
