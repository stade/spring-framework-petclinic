pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        sh 'docker info'
        sh '''which docker
'''
        sh 'docker ps'
      }
    }
    stage('test') {
      steps {
        sh 'mvn test'
      }
    }
    stage('deploy') {
      steps {
        sh 'mvn tomcat7:run-war'
      }
    }
  }
}