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
      parallel {
        stage('package') {
          steps {
            echo 'packaging'
            sh 'mvn package -DskipTests'
          }
        }

        stage('Docker B&P') {
          steps {
            script {
              docker.withRegistry('https://index.docker.io/v1/', 'dockerlogin')
              {
                def commitHash = env.GIT_COMMIT.take(7)
                def dockerImage = docker.build("ej37/sysfoo:${commitHash}", "./")
                dockerImage.push()
                dockerImage.push("latest")
                dockerImage.push("from-jenkins")
              }
            }

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