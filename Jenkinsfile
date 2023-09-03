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
          publishCoverage adapters: [jacocoAdapter('/target/surefire-reports/jacoco.xml')]
        }
      }
    }

    
    }
}
