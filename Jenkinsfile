node {
  def apps

  stage ('Clone Repository') {
    checkout scm
  }

  stage('Build Image') {
    app = docker.build("neargas/Dockerfile")
  }
}
