pipeline {
    agent {
        docker {
            image 'moveho/docker-jenkins-cicd'
            args '-u root'
        }
    }
    stages {
        stage('Build and Push Image') {
            steps {
                sh 'docker build -t moveho/docker-jenkins-cicd:latest .'
                withCredentials([usernamePassword(credentialsId: 'docker-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                }
                sh 'docker tag moveho/docker-jenkins-cicd'
                sh 'docker push moveho/docker-jenkins-cicd'
            }
        }
    }
}
