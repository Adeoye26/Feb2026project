pipeline {

    agent any

    tools {
        jdk 'myjava'
        maven 'mymaven'
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Cloning repository...'
                git 'https://github.com/Adeoye26/Feb2026project.git'
            }
        }

        stage('Compile') {
            steps {
                echo 'Compiling application...'
                sh 'mvn clean compile'
            }
        }

        stage('Code Review') {
            steps {
                echo 'Running code review...'
                sh 'mvn pmd:pmd'
            }
        }

        stage('Unit Test') {
            steps {
                echo 'Running unit tests...'
                sh 'mvn test'
            }

            post {
                success {
                    junit allowEmptyResults: true,
                           testResults: 'server/target/surefire-reports/*.xml'
                }
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging application...'
                sh 'mvn package'
            }

            post {
                success {
                    archiveArtifacts artifacts: 'server/target/*.jar, server/target/*.war',
                                     fingerprint: true

                    echo 'Artifacts archived successfully.'
                }
            }
        }
    }
}
