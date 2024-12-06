pipeline {
    agent any

    environment {
        TF_WORKSPACE = "Testing" // Change to the desired Terraform workspace
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Clone the GitHub repository
                git branch: 'main', url: 'https://github.com/your-username/your-repository.git'
            }
        }

        stage('Terraform Init') {
            steps {
                // Initialize Terraform
                sh 'terraform init'
            }
        }

        stage('Terraform Plan') {
            steps {
                // Generate a plan
                sh 'terraform plan -out=tfplan'
            }
        }

        stage('Terraform Apply') {
            steps {
                // Apply the changes
                input message: "Approve Terraform Apply?", ok: "Apply"
                sh 'terraform apply tfplan'
            }
        }
    }

    post {
        always {
            // Cleanup or notifications
            echo 'Pipeline completed!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
