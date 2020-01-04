pipeline{
    agent none
    stages{
		stage('master'){
		    agent{
			    node{
			    	label 'master'
				    customWorkspace 'e:/jenkins'
		    	}
		    }
        steps{
			powershell label: '', script: '''
				echo "ha"
			'''
			}
		}
    }
    post{
        success{
            echo "success"
        }
	}
}
