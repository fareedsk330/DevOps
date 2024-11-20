pipeline
{
  agent any
  environment{
    DOCKERHUB_CREDS='dockerhub-cred-id'
    IMAGE_NAME= 
    TAG='latest'
    GITHUB_URL='https://github.com/fareedsk330/DevOps.git'
  }
  stages{
    stage("Checkout code"){
      git url: 'GITHUB_URL', branch: 'main'
    }
    stage('build docker image'){
      steps{
        script{
        sh '''
        echo "Building a Docker image"
        docker build -t "${DOCKERHUB_CREDS}:${TAG}"
        '''
      }
      }
    }
    stage('docker login'){
      steps{
      docker.withRegistry("",${DOCKERHUB_CREDS}){
        echo "Successfully logged in to docker"
      }
      }
    }
    stage('pushing docker image'){
      steps{
        docker.withRegistry("", ${DOCKERHUB_CREDS}){
          sh "docker push ${DOCKERHUB_CREDS}:${TAG}"
        }
      }
    }
  }
}   
