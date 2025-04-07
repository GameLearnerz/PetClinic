pipeline {
  agent any
  tools {
    jdk 'JDK21'
    maven 'Maven3'
    nodejs 'Node16'
  }
  stages {
    stage('Checkout') {
      steps {
        git(url: 'https://github.com/mitesh51/spring-petclinic.git', branch: 'master')
      }
    }
    stage('Install Front-End') {
      steps {
        sh 'npm install'
      }
    }
    stage('Build') {
      steps {
        sh './mvnw clean install -Pnpm-install'
      }
    }
    stage('Coverage') {
      steps {
        sh './mvnw jacoco:report'
      }
      post {
        always {
          jacoco(execPattern: '**/target/jacoco.exec')
        }
      }
    }
  }
}