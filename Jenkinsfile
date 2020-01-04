pipeline {
  agent none
  stages {
    stage('master') {
      environment {
        test = '2'
      }
      parallel {
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

        stage('error') {
          agent {
            node {
              label 'master'
            }

          }
          steps {
            sh 'echo "gaga"'
          }
        }

      }
    }

    stage('error') {
      steps {
        echo 'hehe'
      }
    }

  }
  post {
    success {
      echo 'success'
    }

  }
}