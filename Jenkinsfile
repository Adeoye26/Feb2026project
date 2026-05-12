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

                echo 'Cloning repository...'

                git 'https://github.com/Adeoye26/Feb2026project.git'

                stash name: 'source-code', includes: '**/*'
            }
        }

        stage('Compile with agent1') {

            agent { label 'agent1' }

            steps {

                unstash 'source-code'

                echo 'Compiling application...'

                sh 'mvn clean compile'
            }
        }

        stage('CodeReview with agent1') {

            agent { label 'agent1' }

            steps {

                unstash 'source-code'

                echo 'Running code review...'

                sh 'mvn pmd:pmd'
            }
        }

        stage('UnitTest with agent2') {

            agent { label 'agent2' }

            steps {

                unstash 'source-code'

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

        stage('Package on master') {

            agent { label 'master' }

            steps {

                unstash 'source-code'

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
