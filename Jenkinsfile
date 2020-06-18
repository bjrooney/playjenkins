pipeline {

    agent {
    kubernetes {
      label 'test'
      defaultContainer 'jnlp'
      yaml """
apiVersion: v1
kind: Pod
metadata:
labels:
  component: test
spec:
  containers:
  - name: node
    image: node:latest
    command:
    - cat
    tty: true
"""
}
  }

  stages {

    stage('Checkout Source') {
      steps {
          container('test') {
                   git url:'https://github.com/justmeandopensource/playjenkins.git', branch:'test-deploy-stage'
          }
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
