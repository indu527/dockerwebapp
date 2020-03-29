pipeline { 
    agent any

    options {
        skipStagesAfterUnstable()
    }

    environment {
       
        DOCKER_REGISTRY = "https://registry.hub.docker.com"
    }

    stages {

        stage ('Build docker image') { 
            steps {
               script {
                  docker.withRegistry("https://registry.hub.docker.com", 'dockerhub') {
                      def customImage = docker.build("indu527/ngapp")
                customImage.push()
                  }
               }
            }   
        }
        stage('Test'){
            steps {
              bat "echo Testing..."
            }
        }
   }
}