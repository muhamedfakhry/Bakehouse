pipeline {
    agent { label "iti-qena" }

    stages {
        stage('build') {
            steps {
                echo 'build'
                sh "echo ${BUILD_NUMBER}"
            }
        }
        stage('test') {
            steps {
                echo 'test'
                sh """
                    echo "build number is ${BUILD_NUMBER}"
                    curl --help
                """
            }
        }
        stage('publish') {
            steps {
                echo 'publish'
            }
        }
        stage('sonarqube') {
            steps {
                echo 'sonarqube'
            }
        }
        stage('deploy') {
            steps {
                echo 'deploy'
            }
        }
    }
}
