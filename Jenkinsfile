pipeline {
    agent any

    environment {
        IMAGE_NAME = "ubuntu/apache2"
        IMAGE_TAG = "latest"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/vidhipal-2/gs-spring-boot-docker.git'
            }
        }

        stage('Build') {
            steps {
                sh './mvnw clean package'
            }
        }

        stage('Approval') {
            steps {
                script {
                    def userInput = input(id: 'Proceed', message: 'Deploy to Production?', parameters: [choice(choices: ['Yes', 'No'], description: 'Approve deployment?', name: 'approve')])
                    if (userInput == 'No') {
                        error 'Deployment aborted by user'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                sh 'echo "Deploying application..."'
                // Add your deployment script here, e.g., kubectl apply or helm install
            }
        }
    }
}

