pipeline {
    agent {
        node {
            label 'Jenkins-Slave-Node'
        }
    }
    stages {
        stage("checkout Code") {
            steps {
                git url:'https://github.com/ANURAG-DANDGE/jenkins_AVD.git', branch:'main'
            }
        }
             stage("Build Docker image") {
            steps {
                sh 'docker build -t myimage .'
            }
        }
        stage('Add tag and Push Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'anurag0454', passwordVariable: 'wevmSmGwmPhpUlVZjQyWbRAYp4')]) {
                    sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
                    sh 'docker tag myimage $DOCKER_USERNAME/myimage'
                    sh 'docker push $DOCKER_USERNAME/myimage'
                }   
            }
        }
        stage('Deploy application to kubernetes') {
            steps {
                sh 'kubectl apply -f my-deployment.yml'
            }

           }
}
}
