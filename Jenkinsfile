node {
  def app
  def db

  stage ('Clone Repository') {
    checkout scm
  }

  stage('Build Image') {
    db = docker.build("postdb", "-f psql/Dockerfile .").withRun('-e "POSTGRES_PASSWORD=mysecretpassword" "BENCINERA_DATABASE_PASSWORD=mysecretpassword"')

    app = docker.build("neargas","-f neargas/Dockerfile .").withRun('-e "BENCINERA_DATABASE_PASSWORD=mysecretpassword"')
  }
  stage('Testing')
  {
    db.inside.("--link ${db.id}:db")
    app.inside.("--link ${db.id}:db"){
      sh 'echo "HOLAA"
      ping db'
    }
  }
}
