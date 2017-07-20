pipeline {
  agent {
    docker {
      image 'maven:3.5.0-jdk-8'
      args '-v /home/ec2-user/.m2:/root/.m2 -p 9966:9966 '
    }
    
  }
  stages {
    stage('install & build') {
      steps {
        sh 'mvn -Dmaven.test.skip=true install'
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