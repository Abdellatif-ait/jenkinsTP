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

  }
}

}