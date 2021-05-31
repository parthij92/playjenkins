pipeline {

  agent { label 'kubepod' }

  stages {

    stage('Checkout Source') {
      steps {
        git url:'https://github.com/parthij92/playjenkins.git', branch:'test-deploy-stage'
      }
    }
    
    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: 'nginx_1.yaml', kubeconfigId: 'kd_myconfig')
        }
      }
    }
    
  }

}
