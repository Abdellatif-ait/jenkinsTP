pipeline {
  agent any
  parameters {
    string(successMsg: 'Deployed successfully', failureMsg: 'Failed to deploy')
  }
  stages {
    stage ('test') { // la phase test
    post {
      failure {
            notifyEvents message: params.failureMsg, token: 'SzMXDLPEn2TB90mdew7iN6VjO_paqZP0'
      }
    }
    steps {
    bat 'gradle test'
    }
    }
    // archive les résultats des tests
    stage ('archive') {
    post {
      failure {
        notifyEvents message: 'archive failed', token: 'SzMXDLPEn2TB90mdew7iN6VjO_paqZP0'
      }
    }
    steps {
    archiveArtifacts artifacts: 'build/reports/tests/test/index.html'
    }
    }
    // generate the report cucumber
    stage ('report') {
    post {
      failure {
        notifyEvents message: 'report failed', token: 'SzMXDLPEn2TB90mdew7iN6VjO_paqZP0'
      }
    }
    steps {
    cucumber 'build/reports/tests/test/*.json'
    }
    }
   // analyse le code source
    stage ('sonar') {
    post {
      failure {
         notifyEvents message: 'sonar failed', token: 'SzMXDLPEn2TB90mdew7iN6VjO_paqZP0'

      }
    }
    steps {
    withSonarQubeEnv('sonar') {
    bat 'gradle sonarqube'
    }
    }
    }
    // etat de qualité du code
    stage ('quality gate') {
    post {
      failure {
        notifyEvents message: 'quality gate failed', token: 'SzMXDLPEn2TB90mdew7iN6VjO_paqZP0'
      }
    }
    steps {
    waitForQualityGate abortPipeline: true
    }
    }
    // build: genere le jar et genere la documentation et archive le jar et la documentation
    stage ('build') {
    post {
      failure {
            notifyEvents message: 'build failed', token: 'SzMXDLPEn2TB90mdew7iN6VjO_paqZP0'
      }
    }
    steps {
    bat 'gradle build'
    bat 'gradle javadoc'
    archiveArtifacts artifacts: 'build/libs/*.jar'
    archiveArtifacts artifacts: 'build/docs/javadoc/index.html'
    }
    }
    // deploy in mymaevnrepository
    stage ('deploy') {
    post {
      failure {
            notifyEvents message: 'deploy failed', token: 'SzMXDLPEn2TB90mdew7iN6VjO_paqZP0'
      }
    }
    steps {
    withMaven(maven: 'maven3') {
    bat 'gradle publish'
    }
    }
    }
    }
    }
    stage('notify') { // la phase publish
    steps {
    notifyEvents message: params.successMsg, token: 'SzMXDLPEn2TB90mdew7iN6VjO_paqZP0'
    }
    }
    
  }

}

}
