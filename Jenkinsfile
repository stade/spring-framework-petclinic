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
        sh 'mvn test || exit 0'
      }
    }
    stage('publish test results') {
      steps {
        junit '${basedir}/target/surefire-reports'
      }
    }
    stage('deploy') {
      steps {
        sh 'mvn -Dmaven.test.skip=true tomcat7:run-war &'
      }
    }
  }
}