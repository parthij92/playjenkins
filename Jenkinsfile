pipeline {

  agent { label 'kubepod' }

  stages {

    stage('Checkout Source') {
      steps {
        git url:'https://github.com/parthij92/playjenkins.git', branch:'test-deploy-stage'
      }
    }
    
    stage('Apply Kubernetes files') {
      withKubeConfig([credentialsId: 'mykubeconfig') {
        sh 'kubectl apply -f myweb.yaml'
      }
    }
    
  }

}
