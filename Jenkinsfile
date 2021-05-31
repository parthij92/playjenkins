pipeline {

  environment {
    registry = "192.168.0.121:5000/justme/myweb:4"
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
          dockerImage = docker.build registry
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
