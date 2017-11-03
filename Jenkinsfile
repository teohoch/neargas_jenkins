node {

  def app

    stage ('Clone Repository') {
      checkout scm
    }

    stage('Build Image') {
      app = docker.build("neargas","-f neargas/Dockerfile .")
      app.inside{
        sh'''
        rm -rf neargass
        git clone https://github.com/teohoch/neargass.git
        cp neargas/database.yml neargass/config/database.yml
        '''
      }
    }
    stage('Testing')
    {
      app.inside{
        try{
          sh '''
          cd neargass
          bundle exec rspec spec --format html --out rspec_results/results.html --format RspecJunitFormatter --out rspec_results/results.xml
          '''
        }
        finally{
          echo currentBuild.result
          sh'''
          ls
          '''
          junit keepLongStdio: true, testResults: 'rspec_results/*.xml'
        }
      }
    }
    stage('Push to Prod'){
      if (currentBuild.result == null || currentBuild.result == 'SUCCESS') {
        sh '''
        CONTAINERS=$(docker ps -a --filter name=neargas_light --format "{{.Names}}")
                    if ! [ -z "$CONTAINERS" ]
                    then
                         docker restart $CONTAINERS
                    fi
        '''
      }
    }
}
