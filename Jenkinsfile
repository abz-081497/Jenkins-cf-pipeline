@Library('SharedLibrary-Stack') _
pipeline {
    agent any
	
	environment {
            bucketName = "test-cf-bucket-abigael"
			stackFileName = "wp.yaml"
			VpcId = "vpc-0c0aaa01e7b925bed"
			PubSub1 = "subnet-0b6136fa65601f4a3"
			PubSub2 = "subnet-03fce826b630d2558"
    }
	
	parameters { 
		string(
			name: 'ENV', 
			defaultValue: 'DEV', 
			description: 'Please insert the environment'
			)
		string(
			name: 'stackName', 
			defaultValue: 'myStack', 
			description: 'Please insert the stack name'
			)
	}
	
    stages {
     
		stage("Push template to S3") {
			steps {
				uploadFilesToS3(stackFileName: "${stackFileName}", workingDir: "${env.WORKSPACE}/stack_templates", bucketName: "${bucketName}")
			}
		}
		stage('Deploy Stack') {                  
                steps {
                    deploy_stack(stackName: "${stackName}", bucketName: "${bucketName}", stackFileName: "${stackFileName}", env: "${ENV}", VpcId: "${VpcId}", PublicSubnet1: "${PubSub1}", PublicSubnet2: "${PubSub2}")
                }
            }
		
		  
    }
   }
