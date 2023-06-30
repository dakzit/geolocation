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
    
    stage('Upload Artifact') {
      steps {
        script {
          def mavenPom = readMavenPom file: 'pom.xml'
          nexusArtifactUploader artifacts: [[artifactId: "${mavenPom.artifactId}",
                                             classifier: '',
                                             file: "target/${mavenPom.artifactId}-${mavenPom.version}.${mavenPom.packaging}",
                                             type: "${mavenPom.packaging}"]],
                                credentialsId: 'NexusID',
                                groupId: "${mavenPom.groupId}",
                                nexusUrl: 'http://192.168.35.35:8081',
                                nexusVersion: 'nexus2',
                                protocol: 'http',
                                repository: 'biom',
                                version: "${mavenPom.version}"
        }
      }
    }
    
    stage('List Directory') {
      steps {
        sh 'ls'
      }
    }
  }
}
