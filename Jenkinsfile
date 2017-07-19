pipeline {
  agent {
    docker {
      image 'maven:3.5.0-jdk-7-alpine'
      args '-v /tmp/.m2:/root/.m2'
    }
    
  }
  stages {
    stage('build') {
      steps {
        sh 'mvn compile'
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