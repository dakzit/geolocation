pipeline {
    triggers {
        pollSCM('* * * * *')
    }
    agent any
    tools {
        maven 'M2_HOME'
    }

    stages {
        stage("build & SonarQube analysis") {
            agent any
            steps {
                echo 'build & SonarQube analysis...'
                withSonarQubeEnv('sonar') {
                    sh 'mvn verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.projectKey=dakzit_geolocation -X'
                }
            }
        }

        stage('maven package') {
            steps {
                sh 'mvn clean'
                sh 'mvn package -DskipTests'
            }
        }
        
        stage('Build Image') {
            steps {
                script {
                    def mavenPom = readMavenPom file: 'pom.xml'
                    POM_VERSION = "${mavenPom.version}"
                    echo "${POM_VERSION}"
                    dockerImage = docker.build registry + ":${POM_VERSION}"
                }
            }
        }
    }
}
