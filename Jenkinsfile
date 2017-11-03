node {


  stage ('Clone Repository') {
    checkout scm
  }

  stage('Build Image') {
    app = docker.build("neargas","-f neargas/Dockerfile .").withRun('-e "BENCINERA_DATABASE_PASSWORD=mysecretpassword"')
  }
  stage('Testing')
  {
      sh '''
      echo "HOLAA"
      ping hochfarber.com
      '''
    }
  }
