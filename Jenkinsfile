pipeline {
    agent { label "iti-qena" }

    stages {
        stage('build') {
            steps {
                echo 'build'
                
                withCredentials([usernamePassword(credentialsId: 'iti-qena-dockerhub', usernameVariable: 'USERNAME_QENA', passwordVariable: 'PASSWORD_QENA')]) {
                    sh """
                        docker build -t kareemelkasaby/itiqenabakehouse .
                        docker login -u ${USERNAME_QENA} -p ${USERNAME_QENA}
                        docker push kareemelkasaby/itiqenabakehouse 
                    """
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
