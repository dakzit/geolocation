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
    // Add more stages as needed
  }
}
