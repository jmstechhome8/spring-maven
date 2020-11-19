pipeline {
  agent any
  stages {
    stage('scm') {
      steps {
        git(url: 'https://github.com/jmstechhome8/spring-maven.git', branch: 'master')
      }
    }

    stage('maven') {
      steps {
        sh 'mvn package'
      }
    }

  }
}