pipeline {
  agent none
  stages {
    stage('build') {
      agent {
        docker {
          image 'maven:3.9.6-eclipse-temurin-17-alpine'
        }

      }
      steps {
        echo 'Building'
        sh 'mvn compile'
      }
    }

    stage('test') {
      agent {
        docker {
          image 'maven:3.9.6-eclipse-temurin-17-alpine'
        }

      }
      steps {
        echo 'testing'
        sh 'mvn clean test'
      }
    }

    stage('package') {
      agent any
      steps {
        echo 'packaging'
        sh 'mvn package -DskipTests'
      }
    }

  }
  tools {
    maven 'Maven 3.6'
  }
  post {
    always {
      echo 'This pipeline is completed..'
    }

  }
}