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

        // Optional: mvn clean package already runs tests,
        // so you can remove this stage if you don't need
        // to execute tests twice.
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }
        stage('Copy Artifact') {
    steps {
        sh '''
        mkdir -p /Users/sadara/apps/demo

        cp target/demo-0.0.1-SNAPSHOT.war \
           /Users/sadara/apps/demo/
        '''
    }
}
stage('Deploy') {
    steps {
        sh '/Users/sadara/apps/demo/start.sh'
    }
}
stage('Health Check') {
    steps {
        sh '''
        curl -f http://localhost:8081/
        '''
    }
}
    }
}
