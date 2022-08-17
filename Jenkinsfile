pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'docker login https://enes.local.registry:5000/mvcapp:${BUILD_NUMBER}v'
        sh 'docker build github.com/menesunlu/mvcapp_from_ercanesee -t mvcapp:${BUILD_NUMBER}v'
        sh 'docker tag mvcaoo:${BUILD_NUMBER}v enes.local.registry:5000/mvcapp:${BUILD_NUMBER}'
        sh 'docker push enes.local.registry:5000/mvcapp:${BUILD_NUMBER}'
      }
    }

  }
}