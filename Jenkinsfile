pipeline {
    agent any
    
    stages {
        stage('Echo Build Number') {
            steps {
                echo 'Build Number: ' + env.BUILD_NUMBER
            }
        }
        
        stage('List Files') {
            steps {
                sh 'ls'
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed! Notify the team...'
        }
    }
}
