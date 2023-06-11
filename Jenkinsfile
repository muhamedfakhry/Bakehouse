pipeline {
    agent {label "sys-sdmin-mnf"}

    stages {
        stage('build') {
            steps {
                echo 'build'
                withCredentials([usernamePassword(credentialsId: 'iti-sys-admin-mnf-docker-cred', usernameVariable: 'USERNAME_SYSADMIN', passwordVariable: 'PASSWORD_SYSADMIN')]) {
                    sh """
                        docker login -u ${USERNAME_SYSADMIN} -p ${PASSWORD_SYSADMIN}
                        docker build -t kareemelkasaby/bakehouseitisysadmin:v1 .
                        docker push kareemelkasaby/bakehouseitisysadmin:v1
                    """
                }
            }
        }
        stage('deploy') {
            steps {
                echo 'deploy'
                sh "ls"
            }
        }
    }
}
