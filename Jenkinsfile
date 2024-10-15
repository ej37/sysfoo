pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'Building'
        sh 'mvn compile'
      }
    }

    stage('test') {
      steps {
        echo 'testing'
        sh 'mvn clean test'
      }
    }

    stage('package') {
      steps {
        echo 'packaging'
        sh 'mvn package -DskipTests'
      }
    }

    stage('newly-added-stage') {
      parallel {
        stage('newly-added-stage') {
          steps {
            echo 'hey hey'
            sleep 3
          }
        }

        stage('new-stage-2-parallel') {
          steps {
            echo 'see how it goes'
            sleep 2
          }
        }

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