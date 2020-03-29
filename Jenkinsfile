pipeline { 
    agent any

    options {
        skipStagesAfterUnstable()
    }

    environment {
        USERNAME = credentials('DOCKER_USERNAME')
        PASSWORD = credentials('DOCKER_PASSWORD')     
        DOCKER_REGISTRY = "https://registry.hub.docker.com"
        
        
    }

    stages {

        stage ('configuration') {
            steps {
                bat "docker login -u ${USERNAME} -p ${PASSWORD} ${ARTIFACTORY_DOCKER_REGISTRY}"
              
            }
        }
        stage ('Build docker image') { 
            steps {
               script {
                  docker.build("${DOCKER_REGISTRY}" + '/ngapp:latest')
               }
            }   
        }
        stage('Test'){
            steps {
              bat "echo Testing..."
            }
        }
        stage ('Push image to Docker Hub') {
            steps {   
             
                bat "docker tag ngapp ${DOCKER_REGISTRY}/ngapp:latest"
                bat "docker push ${DOCKER_REGISTRY}/ngapp:latest"
            }
        }
   }
}