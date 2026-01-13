@Library('belajar-jenkins-shared-library@main') _

import gilanggustina.jenkins.Output

pipeline {
    agent any

    stages {
        stage('Global Variable from Shared Library') {
            steps {
                script {
                    echo(author())
                    echo("Author Name: ${author.name()}")
                    echo("Author Channel: ${author.channel()}")
                }
            }
        }

        stage('Hello Groovy Class') {
            steps {
                script {
                    Output.hello(this,'Gilang')
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