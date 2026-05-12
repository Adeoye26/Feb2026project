pipeline {

    agent none

    tools {
        jdk 'myjava'
        maven 'mymaven'
    }

    stages {

        stage('Checkout on Master') {
            agent { label 'master' }

            steps {
                echo 'cloning...'
                git 'https://github.com/Adeoye26/Feb2026project.git'

                stash name: 'source-code', includes: '**/*'
            }
        }

        stage('Compile with agent1') {
            agent { label 'agent1' }

            steps {
                unstash 'source-code'

                echo 'compiling...'
                sh 'mvn clean compile'
            }
        }

        stage('CodeReview with agent1') {
            agent { label 'agent1' }

            steps {
                unstash 'source-code'

                echo 'codeReview...'
                sh 'mvn pmd:pmd'
            }
        }

        stage('UnitTest with agent2') {
            agent { label 'agent2' }

            steps {
                unstash 'source-code'

                echo 'Testing...'
                sh 'mvn test'
            }

            post {
                success {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }

        stage('Package on master') {
            agent { label 'master' }

            steps {
                unstash 'source-code'

                echo 'Packaging...'
                sh 'mvn package'
            }

            post {
                success {

                    archiveArtifacts artifacts: 'target/*.jar, target/*.war',
                    fingerprint: true

                    echo 'Artifacts archived successfully'
                }
            }
        }
    }
}
