pipeline {
  agent any
  stages {
    stage ('test') { // la phase test
        post {
        failure {
          script {
            mail= " test termine avec echec "
          }

        }


        success {
          script {
            mail=" test termine avec succes "
          }

        }

      }
      steps {
            bat 'gradle test'
            junit 'build/test-results/test/TEST-Matrix.xml'
              cucumber buildStatus: 'UNSTABLE',
                    reportTitle: 'My report',
                    fileIncludePattern: 'target/*.json',
                    trendsLimit: 10

            }
    }
        stage('Code Analysis') {
                post {
        failure {
          script {
            mail= " Code Analysis termine avec echec "
          }

        }

        success {
          script {
            mail=" Code analysis termine avec succes "
          }

        }

      }

          steps {
            withSonarQubeEnv('sonar') {
              bat 'gradle sonarQube'
            }

            waitForQualityGate true
          }
        }

       stage('Build') {
               post {
        failure {
          script {
            mail= " Build termine avec echec "
          }

        }

        success {
          script {
            mail=" Build termine avec succes "
          }

        }

      }
      steps {
        bat 'gradle build'
        bat 'gradle javadoc'
        archiveArtifacts 'build/libs/*.jar'
        archiveArtifacts 'build/docs/javadoc/**'
      }
    }
        stage('Deployment') {
                post {
        failure {
          script {
            mail= " Deployement terminé avec échec "
          }

        }

        success {
          script {
            mail=" Deployement termine avec succes "
          }
        }

      }
      steps {
        bat 'gradle publish'
        }
       }
        stage('Deployement Notification') {
        steps {
            notifyEvents message: "deployed", token: 'SzMXDLPEn2TB90mdew7iN6VjO_paqZP0'
        }

}//stages

}//pipeline


