pipeline {
  agent any
  stages {
    stage('Compile') {
      steps {
        sh './mvnw clean compile'
      }
    }

    stage('') {
      steps {
        sh '''./mvnw sonar:sonar \\
  -Dsonar.projectKey=Petclinic-1 \\
  -Dsonar.projectName=\'Petclinic-1\' \\
  -Dsonar.host.url=http://172.31.29.130:9000 \\
  -Dsonar.token=sqp_8605bb8c275637212e0a67bed70caa52196bf9c2'''
      }
    }

  }
}