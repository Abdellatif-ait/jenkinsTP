pipeline {
  agent any
  stages {
    stage ('build') { // la phase build
    steps {
    bat 'gradle build'
    }
    }
    stage ('test') { // la phase test
    steps {
    bat 'gradle test'
    }
    }
stage ('deploy') { // la phase deploy
    steps {
    bat 'gradle deploy'
    }
    }
    stage('sonar') { // la phase sonar
    steps {
    bat 'gradle sonarqube'
    }
    }
    stage('notify') { // la phase publish
    steps {
    notifyEvents message: 'Hello <b>world</b>', token: 'SzMXDLPEn2TB90mdew7iN6VjO_paqZP0'
    }
    }
  }

}

}