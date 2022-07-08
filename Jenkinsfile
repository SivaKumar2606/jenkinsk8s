pipeline {

  agent { label 'kubepods' }

  stages {

    stage('SCM Checkout') {
      steps {
        git url:'https://github.com/SivaKumar2606/jenkinsk8s.git', branch:'test1-k8sdeploy'
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
