pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Install') {
      steps {
        bat 'npm install'
      }
    }
    stage('Test') {
      steps {
        //bat 'npm test'
        bat '(set CI=true)&&npm test -- --passWithNoTests'
      }
    }
    stage('Start') {
      when {
        branch 'main'
      }
      steps{
        bat 'npm start'
      }
    }
  }
  post{
    success {
      echo 'Pipeline 성공적으로 완료!'
    }
    failure {
      echo 'Pipeline 실패!'
    }
  }
}
