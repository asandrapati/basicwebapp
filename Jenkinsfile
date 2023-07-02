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
        sh 'docker run hello-world'
        sh 'sudo usermod -a -G docker jenkins'
        sh 'sudo usermod -a -G docker admin'
        sh 'chmod 664 /var/run/docker.sock'
        sh 'chmod 777 /var/run'
        sh 'docker pull gesellix/trufflehog'
        sh 'docker run -t getsellix/trufflehog --json https://github.com/asandrapati/testProject.git > trufflehog'
      }
    }
  }
}
