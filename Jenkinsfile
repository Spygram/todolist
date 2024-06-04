pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials-id')
        APP_IMAGE = 'spygram/todolist'
        IMAGE_TAG = 'latest'
    }


    stages {

        stage("Build") {
            steps {
                echo 'Building the image'
                sh "docker compose up -d"
            }
        }
        stage("Push") {
            echo 'Push image to docker hub'
            steps {
                 script{
                    docker.withRegistry('', 'dockerhub-credentials-id') {
                        sh 'docker push $APP_IMAGE:$IMAGE_TAG'
                    }
                }
            }
        }
        stage("Deploy") {
            steps {
                echo 'Deploying the Container'
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}

