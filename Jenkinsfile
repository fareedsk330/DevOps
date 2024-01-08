pipeline {
    agent any
    options {
     timestamps()
    }
    environment {
       DOCKER_CREDS = credentials('docker-cred')
       DOCKER_IMAGE = 'my-image'
       DOCKER_IMAGE_TAG = 'dummy'
    }
    stages {
        stage('Hello') {
            steps {
               echo "Your Executing ${BUILD_NUMBER}th build"
               sh './hello-world.sh'
            }
        }
       stage ("Build Image"){
             steps {
               script {
                     docker.build("${DOCKER_IMAGE}:${DOCKER_IMAGE_TAG}")
                    }
             }
        }
      stage ("Push Image to DockeHub"){
             steps {
               script {
                    withCredentials([usernamePassword(credentialId: DOCKER_CREDS, usernameVariable: DOCKER_USERNAME, passwordVariable: DOCKER_PASSWORD)]){
                     docker.withRegistry('https://index.docker.io/v1/', 'DOCKER_USERNAME', 'DOCKER_PASSWORD'){
                     docker.image("${DOCKER_IMAGE}:${DOCKER_IMAGE_TAG}")
                    }
                  }
                }
             }
      }
   }
}
