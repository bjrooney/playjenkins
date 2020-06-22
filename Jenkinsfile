pipeline {

  agent { label 'jenkins-jenkins-slave' }

  stages {

    stage('Checkout Source') {
      steps {
        git url:'https://github.com/bjrooney/playjenkins.git', branch:'test-deploy-stage'
      }
    }

    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "nginx.yaml", kubeconfigId: "mykubeconfig")
        }
      }
    }

  }

}
