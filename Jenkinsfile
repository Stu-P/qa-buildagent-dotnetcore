def imageName = 'qa-buildagent-dotnetcore'

pipeline {
	agent  { label 'docker' } 	
//	environment {
//	}

	options { 
		buildDiscarder(logRotator(numToKeepStr: '10', artifactNumToKeepStr: '10'))
		}

	stages {
		stage("Build Docker Image") {
			steps {
				docker.build("${imageName}:${env.BUILD_ID}")
			}
		}				
		stage("Push Image to ECR")  {
		    steps { //, 'ecr:us-east-1:demo-ecr-credentials'
                docker.withRegistry("250658028269.dkr.ecr.ap-southeast-2.amazonaws.com/${imageName}") {
                    docker.image("${imageName}").push('latest')
                }
 			}
		}
	}
}
