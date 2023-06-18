pipeline {
    agent { label "iti-sys-admin-sohaga" }

    stages {
        stage('build') {
            steps {
                echo 'build'
                withCredentials([usernamePassword(credentialsId: 'iti-sys-admin-sohag-docker-cred', usernameVariable: 'USERNAME_SOHAG', passwordVariable: 'PASSWORD_SOHAG')]) {
                    sh '''
                        docker login -u ${USERNAME_SOHAG} -p ${PASSWORD_SOHAG}
                        docker build -t kareemelkasaby/bakehouseitisohag:v${BUILD_NUMBER} .
                        docker push kareemelkasaby/bakehouseitisohag:v${BUILD_NUMBER}
                    '''
                }
            }
        }
        stage('deploy') {
            steps {
                echo 'deploy'
            }
        }
    }
}
