
  pipeline {
    agent any // You can specify the agent based on your requirement. 'any' allows Jenkins to execute the pipeline on any available agent.

    stages {
        stage('Checkout') {
            steps {
                // This step checks out the source code from your repository
                git 'https://github.com/yourusername/yourrepository.git'
            }
        }

        stage('Build') {
            steps {
                // Example: Build your project using Maven
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                // Example: Run unit tests
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                // Example: Deploy your application to a server
                sh 'ssh user@server "deploy_script.sh"'
            }
        }
    }

    post {
        success {
            // This block will execute if the pipeline succeeds
            echo 'Pipeline succeeded! Deploying...'
        }
        failure {
            // This block will execute if the pipeline fails
            echo 'Pipeline failed! Notify the team...'
        }
    }
}
      
