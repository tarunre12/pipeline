pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                git ''
            }
        }

        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Stop & Remove Old Container') {
            steps {
                sh '''
                docker stop Rahul || true
                docker rm Rahul || true
                '''
            }
        }

        stage('Remove Old Image') {
            steps {
                sh '''
                docker rmi tarunreddy || true
                '''
            }
        }

        stage('Docker Image Build') {
            steps {
                sh 'docker build -t ammulu .'
            }
        }

        stage('Docker Deploy') {
            steps {
                sh 'docker run -d -p 2005:8080 --name Reddy ammulu'
            }
        }
    }
}
