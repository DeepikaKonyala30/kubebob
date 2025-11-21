pipeline {
    agent any 

    stages {
        stage('Build') {
            steps {
                script {
                    //login
                    bat 'docker login -u deepzz72206 -p qwerty123'
                    // Build and push Docker image
                    bat 'docker build -t w9-dh-app:latest .'
                    bat 'docker tag w9-dh-app:latest deepzz72206/w9-dh-app:latest'
                    bat 'docker push deepzz72206/w9-dh-app:latest'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    echo 'Running tests...'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Ensure kubectl is pointing to Docker Desktop's cluster
                    bat 'kubectl config use-context docker-desktop'

                    // Apply Kubernetes resources
                    bat 'kubectl apply -f my-kube1-deployment.yaml'
                    bat 'kubectl apply -f my-kube1-service.yaml'

                    echo 'Deploying application to Docker Desktop Kubernetes...'
                }
            }
        }
    }
}
