pipeline {
    agent any

    stages {
        stage('Build and Push Docker Images') {
            steps {
                script {
                    // Build Docker images
                    docker.build('raghavanp08/myapp', '-f app/Dockerfile .')
                    docker.build('raghavanp08/mypostgres', '-f db/Dockerfile .')

                    // Push Docker images to Docker Hub
                    docker.withRegistry('https://registry.hub.docker.com', 'raghavanp08') {
                        docker.image('raghavanp08/myapp').push()
                        docker.image('raghavanp08/mypostgres').push()
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    // Assuming your Kubernetes manifest file is named kubernetes-manifest.yml
                    sh 'kubectl apply -f kubernetes-manifest.yml'
                }
            }
        }
    }
}
