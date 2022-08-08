pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Building'
        sh 'docker login https://enes.local.registry:5000 -u admin -p 12345678'
        git(url: 'https://github.com/menesunlu/mvcapp_from_ercanesee', branch: 'master', credentialsId: 'GITHUB')
        sh 'docker build Dockerfile'
        sh 'docker tag menesunlu/mvcapp:${BUILD_NUMBER}v enes.local.registry:5000/mvcapp:${BUILD_NUMBER}v'
        sh 'docker push enes.local.registry:5000/mvcapp:${BUILD_NUMBER}v'
      }
    }

    stage('Test') {
      steps {
        echo 'Testing'
        waitForQualityGate(credentialsId: 'sonar', webhookSecretId: 'GITHUB', abortPipeline: true)
      }
    }

    stage('Deploy') {
      steps {
        echo 'Deploying'
        sh 'envsubst < ./prod/deployment.yaml | kubectl apply -f -'
        sh 'kubectl apply -f ./prod/service.yaml'
      }
    }

  }
  environment {
    DOCKER_BUILD_NUMBER = '${BUILD_NUMBER}'
  }
}