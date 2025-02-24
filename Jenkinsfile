pipeline {
    agent { label 'dev-server' }
    
    stages {
        stage("Code clone") {
            steps {
                sh "whoami"
                sh "git clone https://github.com/LondheShubham153/django-notes-app.git"
            }
        }
        stage("Code Build") {
            steps {
                sh "docker build -t notes-app:latest ."
            }
        }
        stage("Push to DockerHub") {
            steps {
                withCredentials([string(credentialsId: 'dockerHubCreds', variable: 'DOCKER_PASSWORD')]) {
                    sh "echo $DOCKER_PASSWORD | docker login -u your-dockerhub-username --password-stdin"
                    sh "docker tag notes-app:latest your-dockerhub-username/notes-app:latest"
                    sh "docker push your-dockerhub-username/notes-app:latest"
                }
            }
        }
        stage("Deploy") {
            steps {
                sh "docker run -d -p 8000:8000 your-dockerhub-username/notes-app:latest"
            }
        }
    }
}

