pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }
    environment {
        AWS_ACCOUNT_ID=460132273510
        AWS_DEFAULT_REGION="ap-south-1"
        REPOSITORY_URI = "${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com"
	registryCredential ="demo-admin-user"
    }
   
    stages {

   
        
    // Building Docker images
    stage('Building image') {
      steps{
        script{
          app = docker.build("underwater")
        }
      }
    }
    
    // Tests
    stage('Unit Tests') {
      steps{
        echo 'Empty'
      }
    }
   
    // Uploading Docker images into AWS ECR
    stage('Deploy') {
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
