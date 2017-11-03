node {
  agent { dockerfile { dir 'neargas' additionalBuildArgs '--build-arg BENCINERA_DATABASE_PASSWORD=mysecretpassword' } }

  stages {
    sh '''
    echo "hola"
    ping hochfarber.com
    '''

  }
}
