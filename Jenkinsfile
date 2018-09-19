pipeline {
  agent {
    docker {
      args '--user=root -v /opt/jenkins_files/cacerts:/usr/lib/jvm/java-8-oracle/jre/lib/security/cacerts -v /opt/jenkins_files/.lein:/root/.lein'
      image 'interwaremx/alpine-lein-maven:1.0'
    }

  }
  stages {
    stage('Package') {
      steps {
        sh 'lein jar'
      }
    }
    stage('Publish') {          
      steps {
        withCredentials([usernamePassword(credentialsId: 'IW_CI', usernameVariable: 'IW_USERNAME', passwordVariable: 'IW_PASSWORD')]) {
          sh 'lein deploy interware-3rdparty'
        }
      }
    }
  }
}