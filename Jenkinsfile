pipeline {

  environment {
    registry = "madhan1115/jenkins"
    dockerImage = ""
  }

agent {
    node {
        label 'kubepods'
    }
}
 
  stage('Checkout Source') {
      steps {
        git 'https://github.com/madhan1115/playjenkins.git'
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
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
          kubernetesDeploy(configs: "myweb.yaml", kubeconfigId: "mykubeconfig")
        }
      }
    }

  }

}
