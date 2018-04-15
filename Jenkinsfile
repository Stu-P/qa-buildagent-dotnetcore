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
				script{
				//docker.build("${imageName}:${env.BUILD_ID}")
				docker.build("${imageName}:latest")
				}
			}
		}				
		stage("Push Image to ECR")  {
		    steps { 
                script{ 
					//sh "docker push \"250658028269.dkr.ecr.ap-southeast-2.amazonaws.com/${imageName}:latest\""
					docker.withRegistry("http://250658028269.dkr.ecr.ap-southeast-2.amazonaws.com") {
                    	docker.image("${imageName}").push("latest")

					}
				}
			}
		}
	}
}

