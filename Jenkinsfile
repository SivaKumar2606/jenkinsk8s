pipeline {

  agent { label 'kubepods' }

  stages {

    stage('SCM Checkout') {
      steps {
        git url:'', branch:''
      }
    }

    stage('Deploy K8S App') {
      steps {
        script {
          kubernetesDeploy(configs: "mysitek8s.yaml", kubeconfigId: "mykubeconfig")
        }
      }
    }

  }

}
