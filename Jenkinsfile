pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                     withCredentials([usernamePassword(credentialsId: 'dockerhublogin', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                        dockerImage = docker.build("jobychacko/weather-app:${env.BUILD_ID}")
                    }
                }
            }
        }
        stage('Push to DockerHub') {
            steps {
                script {
                     withCredentials([usernamePassword(credentialsId: 'dockerhublogin', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                        docker.withRegistry('https://registry.hub.docker.com', 'dockerhublogin') {
                            dockerImage.push("${env.BUILD_ID}")
                        }
                    }
                }
            }
        }
    }
}
