pipeline {
    agent {
      node {
          label 'linux && java11' //cari agent dengan label linux dan java11
      }
    }

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
    }

    post {
        always {
            echo 'I will always say Hello again!'
        }
        success {
            echo 'Yes! The pipeline succeeded!'
        }
        failure {
            echo 'Oh no! The pipeline failed.'
        }
        cleanup {
            echo 'Dont care success or failure'
        }
    }
}
