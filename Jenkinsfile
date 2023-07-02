pipeline {
  agent any
  stages {
    stage ("Initialize") {
      steps {
        sh '''
            echo "PATH = ${PATH}"
            echo "M2_HOME = ${M2_HOME}"
        '''
      }
    }
    stage ('Build') {
      steps {
        sh 'mvn clean package'
       }
    }
    stage ('Check-Git-Secrets') {
      steps {
        sh 'pwd'
        sh 'cd /var/run'
        sh 'chown root:docker /var/run'
        sh 'docker run gesellix/trufflehog --json  https://github.com/asandrapati/testProject.git > trufflehog'
        sh 'cat trufflehog'
        
      }
    }
  }
}
