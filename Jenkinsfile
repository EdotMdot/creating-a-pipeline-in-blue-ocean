pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '-p 3000:3000'
    }

  }
  stages {
    stage('Build') {
      when {
        buildingTag()
      }
      steps {
        sh 'npm install'
      }
    }

    stage('Test') {
      when {
        buildingTag()
      }
      steps {
        sh './jenkins/scripts/test.sh'
      }
    }

    stage('Deliver') {
      when {
        buildingTag()
      }
      steps {
        sh './jenkins/scripts/deliver.sh'
        input 'Finished using the web site? (Click "Proceed" to continue)'
        sh './jenkins/scripts/kill.sh'
      }
    }

  }
  environment {
    CI = 'true'
  }
}
