pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/your-username/ci-cd-docker-aws.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-nginx-app .'
            }
        }
        stage('Push to Amazon ECR') {
            steps {
                sh '''
                aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <aws-account-id>.dkr.ecr.us-east-1.amazonaws.com
                docker tag my-nginx-app <aws-account-id>.dkr.ecr.us-east-1.amazonaws.com/my-nginx-app
                docker push <aws-account-id>.dkr.ecr.us-east-1.amazonaws.com/my-nginx-app
                '''
            }
        }
        stage('Deploy to EC2') {
            steps {
                sh 'docker run -d -p 80:80 891376934402.dkr.ecr.us-east-1.amazonaws.com/my-nginx-app'
            }
        }
    }
}

