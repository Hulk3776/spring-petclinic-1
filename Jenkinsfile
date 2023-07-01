pipeline {
  agent {
    node {
      label 'Test'
    }

  }
  stages {
    stage('Compile') {
      steps {
        sh './mvnw clean compile'
      }
    }

    stage('Static Analysis') {
      steps {
        sh '''./mvnw sonar:sonar \\
  -Dsonar.projectKey=Petclinic-1 \\
  -Dsonar.projectName=\'Petclinic-1\' \\
  -Dsonar.host.url=http://172.31.29.130:9000 \\
  -Dsonar.token=sqp_8605bb8c275637212e0a67bed70caa52196bf9c2'''
      }
    }

    stage('Unit Test') {
      steps {
        sh '''./mvnw "-Dtest=**/petclinic/*/*.java" test
'''
      }
    }

    stage('Package') {
      steps {
        sh './mvnw package -DskipTests=true'
      }
    }

    stage('Deploy') {
      parallel {
        stage('Deploy') {
          steps {
            sh '''./mvnw spring-boot:run </dev/null &>/dev/null &
'''
          }
        }

        stage('Integration and Performance Tests') {
          steps {
            sh './mvnw verify'
          }
        }

      }
    }

  }
}