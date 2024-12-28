pipeline {
    agent {
        node {
            label 'jenkins_slave_node1'
        }
    }
    stages {
        stage("checkout Code") {
            steps {
                git url:'https://github.com/sibeshpatel9490/streamlitapp.git', branch:'main'
            }
        }
             stage("Build Docker image") {
            steps {
                sh 'docker build -t myimage .'
            }
        }
        stage('Add tag and Push Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
                    sh 'docker tag myimage $DOCKER_USERNAME/myimage'
                    sh 'docker push $DOCKER_USERNAME/myimage'
                }   
            }
        }
           }
}