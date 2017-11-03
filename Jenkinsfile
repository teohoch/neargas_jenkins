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
      pwd
      ls
      rspec spec --format html --out rspec_results/results.html --format RspecJunitFormatter --out rspec_results/results.xml
      '''

  }
  post {
        always {

                junit keepLongStdio: true, testResults: 'rspec_results/*.xml'

        }
    }
}
