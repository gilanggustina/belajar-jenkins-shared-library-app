@Library('belajar-jenkins-shared-library@main') _

import gilanggustina.jenkins.Output

pipeline {
    agent any

    stages {
        stage('Hello Groovy Class') {
            steps {
                script {
                    Output.hello('Gilang')
                }
            }
        }

        stage('Hello World') {
            steps {
                script {
                    hello.world()
                }
            }
        }
    }
}