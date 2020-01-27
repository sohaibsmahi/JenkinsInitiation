pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'gradle build'
        sh 'gradle javadoc'
        sh 'gradle jar'
        archiveArtifacts 'build/docs/javadoc/**'
        archiveArtifacts 'build/libs/**'
        junit 'build/test-result/test/*.xml'
      }
    }

  }
}