pipeline {
    agent {
      node {
          label 'linux && java11' //cari agent dengan label linux dan java11
      }
    }

    parameters {
        string(name: 'GREETING', defaultValue: 'Hello', description: 'How should I greet you?')
        text(name: 'FEEDBACK', defaultValue: 'Your feedback here...', description: 'Please provide your feedback')
        booleanParam(name: 'DEPLOY', defaultValue: false, description: 'Should we deploy after build?')
        choice(name: 'COLOR', choices: ['Red', 'Green', 'Blue'], description: 'Pick a color')
        password(name: 'SECRET', defaultValue: 'supersecret', description: 'Enter a secret value')
    }

    environment {
        AUTHOR = 'Cahaya Gilang Gustina'
        PROJECT = 'Belajar Jenkins Pipeline'
    }

    // triggers {
    //     cron('*/5 * * * *') //jadwalkan build setiap 5 menit
    // }

    options {
        disableConcurrentBuilds() //nonaktifkan build concurrent
        timeout(time: 2, unit: 'MINUTES') //batasi waktu maksimal 1 jam
        buildDiscarder(logRotator(numToKeepStr: '5')) //simpan build terakhir sebanyak 5
    }

    stages {
        stage('OS Setup') { //Matrix
            matrix {
                axes {
                    axis {
                        name 'OS'
                        values 'Ubuntu', 'CentOS', 'Windows', 'MacOS'
                    }
                    axis {
                        name 'ARC'
                        values '32', '64'
                    }
                }
                excludes {
                    exclude {
                        axis {
                            name 'OS'
                            values 'Windows'
                        }
                        axis {
                            name 'ARC'
                            values '32'
                        }
                    }
                }
                stages {
                    stage('Show OS Info') {
                        steps {
                            echo("Operating System: ${OS}")
                            echo("Architecture: ${ARC}-bit")
                        }
                    }
                }
            }
        }

        stage('Preparation') { //Sequential Stages or Parallel Stages
            // stages { //Sequential Stages
            //     stage('Prepare Java') {
            //         steps {
            //           echo('Preparing Java Environment...')
            //           sleep(5)
            //         }
            //     }
            //     stage('Prepare Maven') {
            //         steps {
            //           echo('Preparing Maven Environment...')
            //           sleep(5)
            //         }
            //     }
            // }
            parallel { //Parallel Stages
                stage('Prepare Java') {
                    steps {
                      echo('Preparing Java Environment...')
                      sleep(5)
                    }
                }
                stage('Prepare Maven') {
                    steps {
                      echo('Preparing Maven Environment...')
                      sleep(5)
                    }
                }
            }
        }

        stage('Parameter Check') {
            steps {
                echo("Greeting: ${params.GREETING}")
                echo("Feedback: ${params.FEEDBACK}")
                echo("Toggle is set to: ${params.TOGGLE}")
                echo("Selected Color: ${params.COLOR}")
                sh('echo "Secret is ${SECRET}" > "secret.txt"')
            }
        }

        stage('Show Info') {
            environment {
              APP = credentials('gilang_rahasia')
            }
            steps {
              echo("Author: ${AUTHOR}")
              echo("Project: ${PROJECT}")
              echo("Start Job: ${env.JOB_NAME}")
              echo("Start Build: ${env.BUILD_NUMBER}")
              echo("Branch Name: ${env.BRANCH_NAME}")
              echo("App Username: ${APP_USR}")
              // echo("App Password: ${APP_PSW}")
              sh('echo "App Password is ${APP_PSW}" > "secret.txt"')
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
            input {
                message 'Are you sure to deploy?'
                ok 'Yes, deploy now!'
                submitter 'pzn'
                parameters {
                    choice(name: 'TARGET_ENV', choices: ['DEV', 'QA', 'PROD'], description: 'Select the target environment for deployment')
                }
            }
            steps {
                echo('Start Deploying...')
                sleep(5)
                echo("Deployed to ${params.TARGET_ENV} environment.")
            }
        }
        stage('Realese') {
            when {
                expression {
                    return params.DEPLOY
                }
            }
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'gilang_rahasia', 
                    usernameVariable: 'USER'
                    passwordVariable: 'PASSWORD', 
                )]) {
                  sh('echo "Realease it with -u $USER -p $PASSWORD" > "release.txt"')
                }
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
