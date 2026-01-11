pipeline {
    agent {
      node {
          label 'linux && java11' //cari agent dengan label linux dan java11
      }
    }

    stages {
        stage('Build') {
            steps {
                echo 'Start Building...'
                sh ('./mvnw clean compile test-compile') //jalankan perintah maven
                echo 'Build Finished!'
            }
        }
        stage('Test') {
            steps {
                echo 'Start Testing...'
                sh ('./mvnw test') //jalankan perintah maven
                echo 'Testing Finished!'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
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
