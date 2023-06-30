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
          nexusArtifactUploader artifacts: [[artifactId: "${POM_ARTIFACTID}",
                                             classifier: '',
                                             file: "target/${POM_ARTIFACTID}-${POM_VERSION}.${POM_PACKAGING}",
                                             type: "${POM_PACKAGING}"]],
                                credentialsId: 'NexusID',
                                groupId: "${POM_GROUPID}",
                                nexusUrl: 'http://192.168.35.35:8081',
                                nexusVersion: 'nexus2',
                                protocol: 'http',
                                repository: 'biom',
                                version: "${POM_VERSION}"
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
