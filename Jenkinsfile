pipeline {
    agent any

    stages {
        stage('codecheckout') {
            steps {
                git url: "https://github.com/Naveenladdu143/python-app.git.git", branch: "main"
            }
        }

        stage('docker-build') {
            steps {
                sh 'docker build -t flask-app:latest .'
                sh 'docker run -d -p 5000:5000 flask-app:latest '
            }
        }

        stage('docker-push') {
            steps {
                withCredentials([usernamePassword(credentialsId: DOCKER_CREDENTIALS, usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh "echo ${DOCKER_PASSWORD} | docker login -u ${DOCKER_USERNAME} --password-stdin ${DOCKER_REGISTRY}"
                    sh "docker tag Naveenladdu/flask-app:latest flask-app:latest.v1"
                    sh "docker push flask-app:latest.v1"
                }
            }
        }
    }
