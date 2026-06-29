pipeline {

    agent any

    tools {
        jdk 'JDK26'
        maven 'Maven3'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

stage('Deploy') {
    steps {
        sh './deploy.sh'
    }
}
        }

    }
}
