pipeline {
    agent any

    stages {
        stage('Build and Push Docker Images') {
            steps {
                script {
                    docker.build('myapp', '-f app/Dockerfile .')
                    docker.build('mypostgres', '-f db/Dockerfile .')
                    docker.withRegistry('https://registry.example.com', 'docker-credentials') {
                        docker.image('myapp').push()
                        docker.image('mypostgres').push()
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    sh 'kubectl apply -f kubernetes-manifest.yml'
                }
            }
        }
    }
}

