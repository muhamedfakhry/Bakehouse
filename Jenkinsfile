pipeline {
    agent any

    stages {
        stage('build') {
            steps {
                echo 'build'
                sh 'ls'
            }
        }
         stage('package') {
            steps {
                echo 'package'
                sh '''
                    echo ${BUILD_NUMBER}
                    echo ${SYS_ADMIN}
                '''
            }
        }
         stage('test') {
            steps {
                echo 'test'
                sh "pwd"
            }
        }
        stage('deploy') {
            steps {
                echo 'deploy'
                sh """
                    cat --help
                """
            }
        }
    }
}
