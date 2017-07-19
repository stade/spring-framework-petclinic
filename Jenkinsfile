pipeline {
  agent {
    docker {
      image 'maven:latest'
      args '-v /home/ec2-user/.m2:/root/.m2'
    }
    
  }
  stages {
    stage('install & build') {
      steps {
        sh 'mvn -Dmaven.test.skip=true install'
        sh 'mvn build'
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