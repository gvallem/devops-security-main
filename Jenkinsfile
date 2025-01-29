pipeline {
  agent any

  stages {
     stage('Build Artifact - Maven') {
      steps {
        sh "mvn clean package -DskipTests=true"
        archive 'target/*.jar'
      }
    }

    stage('Unit Tests - JUnit and Jacoco') {
      steps {
        sh "mvn test"
      }
      post {
        always {
          junit 'target/surefire-reports/*.xml'
          jacoco execPattern: 'target/jacoco.exec'
        }
      }
    }
    //Docker Build and Push
    stage('Docker Build and Push') {
      steps {
        withDockerRegistry([credentialsId: "docker-hub", url: ""]) {
          sh 'printenv'
          sh 'docker build -t gvallem01/numeric-app:""$GIT_COMMIT"" .'
          sh 'docker push gvallem01/numeric-app:""$GIT_COMMIT""'
        }
      }
    }
    
    
    }
}
