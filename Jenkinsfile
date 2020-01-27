pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'gradle build'
        bat 'gradle javadoc'
        bat 'gradle jar'
        archiveArtifacts 'build/docs/javadoc/**'
        archiveArtifacts 'build/libs/**'
        junit 'build/test-result/test/*.xml'
      }
    }

  }
}