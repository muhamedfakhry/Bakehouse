pipeline {
    agent { label "iti-qena" }
    
    parameters {
        choice(name: 'ENV', choices: ['dev', 'test', 'prod',"release"])
    }
    stages {
        stage('build') {
            steps {
                echo 'build'
                script {
                    if (params.ENV == "release") {
                        withCredentials([usernamePassword(credentialsId: 'iti-qena-dockerhub', usernameVariable: 'USERNAME_QENA', passwordVariable: 'PASSWORD_QENA')]) {
                            sh """
                                docker build -t kareemelkasaby/itiqenabakehouse:${BUILD_NUMBER} .
                                docker login -u ${USERNAME_QENA} -p ${PASSWORD_QENA}
                                docker push kareemelkasaby/itiqenabakehouse:${BUILD_NUMBER}
                                echo ${BUILD_NUMBER} > ../bakehouse-build-number.txt
                            """
                        }
                    }
                }
            }
        }
        stage('deploy') {
            steps {
                echo 'deploy'
                script{
                    if (params.ENV == "dev" || params.ENV == "test" || params.ENV == "prod") {
                        withCredentials([file(credentialsId: 'iti-qena-kubeconfig', variable: 'KUBECONFIG')]) {
                            sh """
                              export BUILD_NUMBER=\$(cat ../bakehouse-build-number.txt)
                              cp Deployment/deploy.yaml Deployment/deploy.yaml.tmp
                              cat Deployment/deploy.yaml.tmp | envsubst > Deployment/deploy.yaml
                              rm -f Deployment/deploy.yaml.tmp
                              kubectl apply -f Deployment --kubeconfig=${KUBECONFIG}
                            """
                        }
                    }
                }
            }
        }
    }
}
