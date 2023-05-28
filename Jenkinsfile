pipeline {
    agent any

    stages {
        stage('test') {
            steps {
                echo 'test'
                sh "ls"
            }
        }
        stage('build') {
            steps {
                echo 'build'
                sh '''
                    docker --help
                    echo ${BUILD_NUMBER}
                    echo 'l jenkins 7elw w bsemsm'
                '''
            }
        }
        stage('deploy') {
            steps {
                echo 'deploy'
                sh "echo 'a7la dof3a de wla eh'"
            }
        }
    }
}
