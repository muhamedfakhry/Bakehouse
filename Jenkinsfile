ipeline {
    agent {
        label 'fakhry'
    }

    stages {
        stage('build') {
            when { 
                anyOf { branch 'dev' ;  branch 'test' ;  branch 'release' }
            }
            steps {
                echo 'build'
                withCredentials([usernamePassword(credentialsId: 'dockerhub-yassmin', usernameVariable: 'DOCKERHUB_USERNAME', passwordVariable: 'DOCKERHUB_PASSWORD')]) {
                    sh '''
                    docker build -t yassmin970/bakehouseyassmin:v${BUILD_NUMBER}-${BRANCH_NAME} .
                    docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD
                    docker push yassmin970/bakehouseyassmin:v${BUILD_NUMBER}-${BRANCH_NAME}
                    '''
                }
            }
        }       
       stage('deploy') {
           when { 
                anyOf { branch 'dev' ;  branch 'test' ;  branch 'release' }
            }
            steps {
                echo 'deploy'
                withCredentials([file(credentialsId: 'kubeconfig-cred', variable: 'KUBECONFIG_YASSMIN')]) {
                    sh '''
                     cat Deployment/deploy.yaml | envsubst > Deployment/deploy.yaml.temp
                     mv Deployment/deploy.yaml.temp Deployment/deploy.yaml
                     kubectl apply -f Deployment --kubeconfig $KUBECONFIG_YASSMIN  -n ${BRANCH_NAME}  
   
                    '''
                }
                }
            }    
        
    }
}    
