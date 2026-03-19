pipeline {
    agent any

    tools {
        jdk 'myjava'
        maven 'mymaven'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'cloning..'
                git 'https://github.com/Adeoye26/Feb2026project.git'
            }
        }

        stage('Compile') {
            steps {
                echo 'compiling..'
                sh 'mvn compile'
            }
        }

        stage('CodeReview') {
            steps {
                echo 'codeReview'
                sh 'mvn pmd:pmd'
            }
        }
    }
}
