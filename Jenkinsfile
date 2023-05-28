pipeline {
    agent { label 'iti-smart' }

    stages {
        stage('build') {
            steps {
                echo 'build'
                script{
                    withCredentials([usernamePassword(credentialsId: 'iti-smart-dockerhub', usernameVariable: 'USERNAME_ITI', passwordVariable: 'PASSWORD_ITI')]) {
                        sh '''
                            docker login -u ${USERNAME_ITI} -p ${PASSWORD_ITI}
                            docker build -t kareemelkasaby/bakehouseitismart:v1 .
                            docker push kareemelkasaby/bakehouseitismart:v1
                        '''
                    }
                }
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
