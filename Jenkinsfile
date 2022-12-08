pipeline {
    agent any
    environment {
        AWS_ACCOUNT_ID=460132273510
        AWS_DEFAULT_REGION="ap-south-1"
	CLUSTER_NAME="devcluster"
	SERVICE_NAME="nodejs-container-service"
	TASK_DEFINITION_NAME="first-run-task-definition"
	DESIRED_COUNT=1
        IMAGE_REPO_NAME="container-repo"
        IMAGE_TAG="${env.BUILD_ID}"
        REPOSITORY_URI = "${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com/${IMAGE_REPO_NAME}"
	registryCredential ="demo-admin-user"
    }
   
    stages {

    // Tests
    stage('Unit Tests') {
      steps{
        echo 'Empty'
      }
    }
        
    // Building Docker images
    stage('Building image') {
      steps{
        script{
          app = docker.build("underwater")
        }
      }
    }
   
    // Uploading Docker images into AWS ECR
    stage('Pushing to ECR') {
     steps{  
         script {
			docker.withRegistry("https://" + REPOSITORY_URI, "ecr:${AWS_DEFAULT_REGION}:" + registryCredential) {
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                	}
         }
        }
      }
      
    
      }      
      
    }
