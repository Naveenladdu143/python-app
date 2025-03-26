pipeline {
    agent any

    stages {
        stage('codecheckout') {
            steps {
                git url: "https://github.com/Naveenladdu143/two-tier-flask-app-master-MattsDevops.git", branch: "jenkins"
            }
        }

        stage('docker-build') {
            steps {
                sh 'docker build -t flask-app:latest .'
                sh 'docker run -d -p flask-app:latest '
            }
        }

        stage('docker-push') {
            steps {
                withCredentials([usernamePassword(credentialsId: DOCKER_CREDENTIALS, usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh "echo ${DOCKER_PASSWORD} | docker login -u ${DOCKER_USERNAME} --password-stdin ${DOCKER_REGISTRY}"
                    sh "docker tag Naveenladdu/flask-app:latest"
                    sh "docker push flask-app"
                }
            }
        }
    }
