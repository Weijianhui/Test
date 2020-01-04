pipeline{
    agent none
    stages{
        /* 1 */
        stage('version0.1'){
			when {environment name: 'version', value: '0.1'}
			stages('run0.1'){
				stage('0.1'){
					agent{
						node{
							label 'master'
							customWorkspace 'e:/jenkins/test'
						}
					}
					/*清理代码文件夹和临时目录*/
					steps{
						bat '''
						echo "run 0.1 stage"
						'''
					}
				}
			}
		}
		stage('version0.2'){
			when {environment name: 'version', value: '0.2'}
			stages('run0.2'){
				stage('0.2'){
					agent{
						node{
							label 'master'
							customWorkspace 'e:/jenkins/test'
						}
					}
					/*清理代码文件夹和临时目录*/
					steps{
						bat '''
						echo "run 0.2 stage"
						'''
					}
				}
			}
		}
		stage('rollback'){
			when {environment name: 'version', value: 'rollback'}
			stages('rollback'){
				stage('mode'){
					input{
						message '输入回滚方式'
						id 'rollback'
						parameters {
							choice choices: ['tag', 'commitId'], description: '', name: 'rollbackmode'
						}
					}
					stages('mode'){
						stage('tag'){
							when {environment name: 'rollbackmode', value: 'tag'}
							stages{
								stage('tag'){
									agent{
										node{
											label 'master'
											customWorkspace 'e:/Jenkins/test'
										}
									}
									input {
										message '输入tag名称'
										id 'tagname'
										parameters {
											string defaultValue: '', description: '', name: 'tag', trim: false
										}
									}
									steps{
										bat "echo $tag"
										checkout([$class: 'GitSCM', branches: [[name: "$tag"]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], 
											userRemoteConfigs: [[credentialsId: 'a1a3829c-a518-4f84-bb83-f781a213c9fd', 
											url: 'http://192.168.1.176:81/zqnb/bug']]])
										bat '''
										echo "run tag stage"
										'''
									}
								}
							}
						}
						stage('commitId'){
							when {environment name: 'rollbackmode', value: 'commitId'}
							stages('commitId'){
								stage('commitId'){
									agent{
										node{
											label 'master'
											customWorkspace 'e:/Jenkins/test'
										}
									}
									input {
										message '输入commitId'
										id 'tagname'
										parameters {
											string defaultValue: '', description: '', name: 'commitId', trim: false
										}
									}
									steps{
										bat "echo $commitId"
										checkout([$class: 'GitSCM', branches: [[name: "$commitId"]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], 
											userRemoteConfigs: [[credentialsId: 'a1a3829c-a518-4f84-bb83-f781a213c9fd', 
											url: 'http://192.168.1.176:81/zqnb/bug']]])
										bat '''
										echo "run commitId stage"
										'''
									}
								}
							}
						}
					}
				}
			}
        }
    }
    post{
        success{
            echo 'when success do'
        }
    }
}
