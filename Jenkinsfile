pipeline {
  agent any
  stages {
    stage('checkout code') {
      steps {
        git(url: 'https://github.com/pooya-dehghan/srttu-jenkins-101', branch: 'develop')
      }
    }

    stage('log') {
      steps {
        sh 'ls'
      }
    }

  }
}