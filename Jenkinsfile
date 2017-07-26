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
      }
    }
    stage('test') {
      steps {
        sh 'mvn test'
      }
    }
    stage('confirm deploy') {
      steps {
        input 'Tests passed. Ready to deploy'
      }
    }
    stage('deploy') {
      steps {
        sh 'mvn -Dmaven.test.skip=true tomcat7:run-war &'
      }
    }
    stage('Create archive & archive') {
      steps {
        sh 'mvn -Dmaven.test.skip=true package '
        archiveArtifacts 'target/*.war'
      }
    }
  }
}