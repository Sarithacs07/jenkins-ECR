pipeline {
    agent any
     environment {
        registry = "957395246111.dkr.ecr.us-east-1.amazonaws.com/demo-ecr-repo"
    }
   
    stages {
          stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Meenakshi0812/jenkins-ECR.git'
            }
        }
           stage('Building image') {
             steps{
                  script {
                   dockerImage = docker.build registry
                   }
      }
           }
    
            stage('Pushing to ECR') {
             steps{  
                  script {
               withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'gsaritha313@gmail.com', accessKeyVariable: 'AKIA552JUDQPVLF4WIFI', secretKeyVariable: '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']]) {
    sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 957395246111.dkr.ecr.us-east-1.amazonaws.com'
     sh 'docker push 957395246111.dkr.ecr.us-east-1.amazonaws.com/<demo-ecr-repo>'
}

}
                  }
            }
            
            stage('Docker Run') {
              steps{
                   script {
                sh 'docker run -d -p 8096:5000 --rm --name mypythonContainer 957395246111.dkr.ecr.us-east-1.amazonaws.com/<demo-ecr-repo>:latest'     
      }
    }
        }
    }
  }
