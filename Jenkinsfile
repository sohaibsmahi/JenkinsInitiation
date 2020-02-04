pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'gradle build'
        bat 'gradle javadoc'
        archiveArtifacts 'build/docs/javadoc/**'
        archiveArtifacts 'build/libs/*.jar'
        junit 'build/test-results/test/*.xml'
      }
    }

    stage('Mail Notification') {
      steps {
        mail(subject: 'Push Github', body: 'Your project have been pushed to the github repo', to: 'gn_farah@esi.dz')
      }
    }

    stage('Code Analysis') {
      parallel {
        stage('Code Analysis') {
          steps {
            withSonarQubeEnv('sonar') {
              bat 'gradle sonarqube'
            }

            waitForQualityGate true
          }
        }

        stage('Test Reporting') {
          steps {
            jacoco(execPattern: 'build/jacoco/test.exec')
          }
        }

      }
    }

    stage('Deployment') {
      when{
        branch 'master'
      }
      steps {
        bat 'gradle publish'
      }
    }

    stage('Slack Notification') {
      when{
        branch 'master'
      }
      steps {
        slackSend(token: 'TRQRD8P16/BSUHJ98P3/H1NKPYpNTdZqAakXQkSCwYFo', teamDomain: 'tpgradleworkspace', baseUrl: 'https://hooks.slack.com/services/', message: 'Your project have been pushed to the github repo', channel: '#general')
      }
    }

  }
}