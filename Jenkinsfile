pipeline {
  agent any

  stages {
      stage('Build Artifact') {
            steps {
              //sh "mvn clean package -DskipTests=true"
              sh "mvn -v"
              //archive 'target/*.jar' //so that they can be downloaded later
            }
        }
        stage('git version') {
          steps {
            sh "git version"
          }
        }
        stage('docker version') {
          steps {
            sh "docker -v"
          }
        }
    
    }
}
