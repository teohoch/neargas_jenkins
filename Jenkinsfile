pipeline {

  def app
  stages {
    stage ('Clone Repository') {
      checkout scm
    }

    stage('Build Image') {
      app = docker.build("neargas","-f neargas/Dockerfile .")
    }
    stage('Testing')
    {
      app.inside{
        sh '''
        bundle exec rspec spec --format html --out rspec_results/results.html --format RspecJunitFormatter --out rspec_results/results.xml
        '''
      }
    }
    stage('Push to Prod'){
      sh '''
      CONTAINERS=$(docker ps -a --filter name=neargas_light --format "{{.Names}}")
                  if ! [ -z "$CONTAINERS" ]
                  then
                       docker restart $CONTAINERS
                  fi
      '''
    }
  }
  post {
        always {

                junit keepLongStdio: true, testResults: 'rspec_results/*.xml'

        }
    }
}
