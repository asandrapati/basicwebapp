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
        sh 'sudo docker run hello-world -S'
        sh 'sudo usermod -a -G docker jenkins'
        sh 'sudo usermod -a -G docker admin'
        sh 'sudo chmod 664 /var/run/docker.sock'
        sh 'sudo chmod 777 /var/run'
        sh 'sudo docker pull gesellix/trufflehog -S'
        sh 'sudo docker run -t getsellix/trufflehog --json https://github.com/asandrapati/testProject.git > trufflehog'
      }
    }
  }
}
