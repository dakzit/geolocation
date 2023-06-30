pipeline {
  agent any
  tools {
    maven 'M2_HOME'
  }
  stages {
    stage('Maven Build') {
      steps {
        sh 'mvn clean install package'
      }
    }
    
    stages {
    stage('Check pwd') {
      steps {
        sh 'pwd'
      }
    }
    stages {
    stage('List Directory') {
      steps {
        sh 'ls'
      }
    }
  }
}
