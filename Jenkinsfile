pipeline {
  agent any
  stages {
    stage('checkout') {
      steps {
        git(url: 'https://github.com/pooya-dehghan/srttu-jenkins-101', branch: 'srttu')
      }
    }

    stage('loging') {
      steps {
        sh 'ls && cat temp.txt'
      }
    }

  }
}