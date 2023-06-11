pipeline {
    agent {label "sys-sdmin-mnf"}

    stages {
        stage('build') {
            steps {
                echo 'build'
                withCredentials([usernamePassword(credentialsId: 'iti-sys-admin-mnf-docker-cred', usernameVariable: 'USERNAME_SYSADMIN', passwordVariable: 'PASSWORD_SYSADMIN')]) {
                    sh """
                        docker login -u ${USERNAME_SYSADMIN} -p ${PASSWORD_SYSADMIN}
                        docker build -t kareemelkasaby/bakehouseitisysadmin:v${BUILD_NUMBER} .
                        docker push kareemelkasaby/bakehouseitisysadmin:v${BUILD_NUMBER}
                    """
                }
            }
        }
        stage('deploy') {
            steps {
                echo 'deploy'
                withCredentials([file(credentialsId: 'iti-sys-admin-mnf-kubeconfig-cred', variable: 'KUBECONFIG_ITI')]) {
                    sh """
                        kubectl apply -f Deployment --kubeconfig ${KUBECONFIG_ITI}
                    """
                }
            }
        }
    }
}
