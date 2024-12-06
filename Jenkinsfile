pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID = credentials('aws-credentials') // Use Jenkins Credentials for AWS
        AWS_SECRET_ACCESS_KEY = credentials('aws-credentials')
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Clone your Git repository
                git branch: 'master', url: 'https://github.com/poorvajanihira/Terraform_Jenkins.git'
            }
        }

        stage('Terraform Init') {
            steps {
                // Initialize Terraform in the workspace
                sh 'terraform init'
            }
        }

        stage('Terraform Plan') {
            steps {
                // Show the planned changes
                sh 'terraform plan -out=tfplan'
            }
        }

        stage('Terraform Apply') {
            steps {
                // Apply the planned changes
                sh 'terraform apply -auto-approve tfplan'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished!'
        }
        failure {
            echo 'Pipeline failed. Check logs for details.'
        }
    }
}
