node {


  stage ('Clone Repository') {
    checkout scm
  }

  stage('Build Image') {
    app = docker.build("neargas","-f neargas/Dockerfile .")
  }
  stage('Testing')
  {
      sh '''
      echo "HOLAA"
      ping hochfarber.com
      '''
    }
  }
