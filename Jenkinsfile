pipeline {
    agent {
      node {
          label 'linux && java11' //cari agent dengan label linux dan java11
      }
    }
    environment {
        AUTHOR = 'Cahaya Gilang Gustina'
        PROJECT = 'Belajar Jenkins Pipeline'
    }
    stages {
        environment {
          APP = credentials('gilang_rahasia')
        }
        stage('Preparation') {
            steps {
              echo("Author: ${AUTHOR}")
              echo("Project: ${PROJECT}")
              echo("Start Job: ${env.JOB_NAME}")
              echo("Start Build: ${env.BUILD_NUMBER}")
              echo("Branch Name: ${env.BRANCH_NAME}")
              echo("App Username: ${APP_USR}")
              echo("App Password: ${APP_PSW}")
            }
        }
        stage('Build') {
            steps {
                // echo('Start Building...')
                // // sh('./mvnw clean compile test-compile') //jalankan perintah maven
                // echo('Build Finished!')
                script {
                  for (int i = 0; i < 5; i++) {
                      echo "Building... iteration ${i}"
                  }
                }
            }
        }
        stage('Test') {
            steps {
                // echo('Start Testing...')
                // // sh('./mvnw test') //jalankan perintah maven
                // echo('Testing Finished!')

                script {
                  def data = [
                    "firstName": "John",
                    "lastName" : "Doe",
                  ]
                  writeJSON(file : 'data.json', json: data, pretty: 4)
                }

            }
        }
        stage('Deploy') {
            steps {
                echo('Deploying...')
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
