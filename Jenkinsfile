
pipeline {

  agent any

  stages {

    stage('SCM Checkout') {
      steps {
        git url:'https://github.com/SivaKumar2606/jenkinsk8s.git', branch:'dev1-k8sdeploy'
      }
    }

    stage('Build image') {
      steps{
       sh "docker build -t sivakumar2606/k8nginxcicd:$BUILD_NUMBER"
      }
    }

    stage('Pushing Image') {
      steps{
        script {
          withCredentials([usernamePassword(credentialsId: 'mydockerhublogin', passwordVariable: 'docker_paswd', usernameVariable: 'docker_user')]) {
            sh "docker login -u $docker_user -p $docker_paswd"  
              }
          }
          sh "docker push sivakumar2606/k8nginxcicd:$BUILD_NUMBER"
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
