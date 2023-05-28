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
                            docker build -t kareemelkasaby/bakehouseitismart:v${BUILD_NUMBER} .
                            docker push kareemelkasaby/bakehouseitismart:v${BUILD_NUMBER}
                        '''
                    }
                }
            }
        }
        stage('deploy') {
            steps {
                echo 'deploy'
                script {
                    withCredentials([file(credentialsId: 'iti-samrt-kubeconfig', variable: 'KUBECONFIG_ITI')]) {
                        sh '''
                            tmp=$(cat Deployment/deploy.yaml | envsubst) && echo ${tmp} > Deployment/deploy.yaml
                            kubectl apply -f Deployment --kubeconfig ${KUBECONFIG_ITI}
                        '''
                    }
                }
            }
        }
    }
}
