pipeline {
    agent any

    tools {
        jdk 'myjava'
        maven 'mymaven'
    }

    stages {

        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }

        stage('Code Review') {
            steps {
                sh 'mvn pmd:pmd'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
    }
}

