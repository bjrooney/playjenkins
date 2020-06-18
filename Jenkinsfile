pipeline {

    agent {
    kubernetes {
      label 'kubepod'
      defaultContainer 'jnlp'
      yaml """
apiVersion: v1
kind: Pod
metadata:
labels:
  component: test
spec:
  containers:
  - name: golang
    image: golang:1.10
    command:
    - cat
    tty: true
"""
}
  }

  stages {

    stage('Checkout Source') {
      steps {
          container('golang') {
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
