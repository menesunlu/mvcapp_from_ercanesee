pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'docker login https://bshregistrysrv:5000 -u admin -p BshDockers14Aw'
        sh 'docker build github.com/menesunlu/mvcapp_from_ercanesee -t mvcapp:${BUILD_NUMBER}v'
        sh 'docker tag mvcapp:${BUILD_NUMBER}v bshregistrysrv:5000/mvcapp:${BUILD_NUMBER}'
        sh 'docker push bshregistrysrv:5000/mvcapp:${BUILD_NUMBER}'
      }
    }

    stage('Deployment') {
      steps {
        sh 'echo ${DOCKER_BUILD_NUMBER}'
        sh 'envsubst < ./prod/deployment.yaml | kubectl apply -f -'
        sh 'kubectl apply -f ./prod/service.yaml'
      }
    }

  }
  environment {
    DOCKER_BUILD_NUMBER = 'BUILD_NUMBER'
  }
}