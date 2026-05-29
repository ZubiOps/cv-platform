pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                sh 'docker build -t zubiops/cv-site:v1 ./app'
            }
        }

        stage('Test') {
            steps {
                sh 'docker run -d -p 8081:80 --name test-cv zubiops/cv-site:v1'
                sh 'sleep 5'
                sh 'docker exec test-cv curl localhost'
                sh 'docker rm -f test-cv'
            }
        }

        stage('Push') {
            steps {
                sh 'docker push zubiops/cv-site:v1'
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker rm -f live-cv || true'
                sh 'docker run -d -p 8090:80 --name live-cv zubiops/cv-site:v1'
            }
        }
    }
}
