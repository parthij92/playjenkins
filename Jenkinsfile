pipeline {

  environment {
    registry = "192.168.0.121:5000/justme/myweb"
    dockerImage = ""
  }

  agent { label 'kubepod' }

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/parthij92/playjenkins.git'
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    
    stage('replace content') {
      steps{
        script {
          contentReplace(configs: [fileContentReplaceConfig(configs: [fileContentReplaceItemConfig(matchCount: 0, replace: '/myweb:$BUILD_NUMBER', search: '/myweb:\\d+')], fileEncoding: 'UTF-8', filePath: 'myweb.yaml')])
        }
      }
    }
    
    

    stage('Push Image') {
      steps{
        script {
          docker.withRegistry( "" ) {
            dockerImage.push()
          }
        }
      }
    }

    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "myweb.yaml", kubeconfigId: "kubeconfig")
        }
      }
    }

  }

}
