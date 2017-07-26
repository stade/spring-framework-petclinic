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
    stage('generate archive') {
      steps {
        sh 'mvn -Dmaven.test.skip=true package '
        archiveArtifacts 'target/*.war'
      }
    }
    stage('publish to s3') {
      steps {
        withAWS(credentials: 's3aws', region: 'eu-west-1') {
          s3Upload(bucket: 'dummy-demo-test-bucket', file: 'target/petclinic.war', path: 'archives/petclinic-"${env.BUILD_ID}".war')
        }
        
      }
    }
  }
}