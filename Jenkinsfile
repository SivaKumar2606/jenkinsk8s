
pipeline {

  environment {
    dockerimagename = "sivakumar2606/k8nginxcicd"
    dockerImage = ""
  }

  agent any

  stages {

    stage('SCM Checkout') {
      steps {
        git url:'https://github.com/SivaKumar2606/jenkinsk8s.git', branch:'dev1-k8sdeploy'
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build dockerimagename + ":$BUILD_NUMBER"
        }
      }
    }

    stage('Pushing Image') {
      environment {
               registryCredential = 'mydockerhublogin'
           }
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }

    stage('Deploying App to Kubernetes') {
      steps {
        script {
          kubernetesDeploy(configs: "mysitek8s-dev.yaml", kubeconfigId: "mykubeconfig")
        }
      }
    }

  }

}
