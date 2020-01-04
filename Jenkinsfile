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

        stage('parl') {
          agent {
            node {
              label 'master'
            }

          }
          steps {
            powershell 'echo \'gaga\''
          }
        }

      }
    }

    stage('end') {
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