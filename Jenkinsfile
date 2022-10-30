pipeline {
  agent { label 'jenkins-ubuntu-slave' }
  parameters {
        choice(name: 'ENV', choices: ['dev', 'test', 'prod',"release"])
  }
  stages {
    stage('build') {
      steps {
        script {
          if (params.ENV == "release") {
            withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
              sh """
                  docker login -u ${USERNAME} -p ${PASSWORD}
                  docker build -t kareemelkasaby/vfbakehouse:${BUILD_NUMBER} .
                  docker push kareemelkasaby/vfbakehouse:${BUILD_NUMBER}
              """
            }
          }
        }
      }
    }
    stage('deploy') {
      steps {
        script {
          sh """
              mv Deployment/deploy.yaml Deployment/deploy.yaml.tmp
              cat Deployment/deploy.yaml.tmp | envsubst > Deployment/deploy.yaml
              rm -f Deployment/deploy.yaml.tmp
              kubectl apply -f Deployment
            """
        }
      }
    }
  }
}
