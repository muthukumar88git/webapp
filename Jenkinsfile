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

        sh '''

            pkill -f demo-0.0.1-SNAPSHOT.war || true

            BUILD_ID=dontKillMe \

            nohup java -jar target/demo-0.0.1-SNAPSHOT.war \

                --server.port=8081 \

                > app.log 2>&1 < /dev/null &

            sleep 2

            exit 0

        '''

    }
}
        }

    

