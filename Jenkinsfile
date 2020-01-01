def imageName = 'qa-buildagent-dotnetcore'
def accId = xxx;

pipeline {
	agent  { label 'docker' } 	

	options { 
		buildDiscarder(logRotator(numToKeepStr: '10', artifactNumToKeepStr: '10'))
		}

	stages {
		stage("Build Docker Image") {
			steps {
				script{
					docker.build("${imageName}:latest")
				}
			}
		}				
		stage("Push Image to ECR")  {
			steps { 
				script{ 
					sh "echo $PATH"
					docker.withRegistry("http://${accId}.dkr.ecr.ap-southeast-2.amazonaws.com") {
                    	docker.image("${imageName}").push("latest")
					}
				}
			}
		}
	}
}

