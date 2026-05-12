pipeline {

    tools {
        jdk 'myjava'
        maven 'mymaven'
    }

    agent any

    stages {

        stage('Checkout on Master') {

            agent any

            steps {
                echo 'cloning...'
                git 'https://github.com/Adeoye26/Feb2026project.git'
            }
        }

        stage('Compile with agent1') {

            agent { label 'agent1' }

            steps {
                echo 'compiling...'
                sh 'mvn compile'
            }
        }

        stage('CodeReview with agent1') {

            agent { label 'agent1' }

            steps {
                echo 'codeReview...'
                sh 'mvn pmd:pmd'
            }
        }

        stage('UnitTest with agent2') {

            agent { label 'agent2' }

            steps {
                echo 'Testing'
                sh 'mvn test'
            }

            post {
                always {
                    junit allowEmptyResults: true,
                           testResults: 'server/target/surefire-reports/*.xml'
                }
            }
        }

        stage('Package on master') {

            agent {
                label 'master'
            }

            steps {

                echo 'Packaging...'

                sh 'mvn package'

                archiveArtifacts artifacts: 'server/target/*.jar',
                                 fingerprint: true
            }
        }
    }
}
