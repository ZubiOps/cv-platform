pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t zubiops/cv-site:v1 .'
            }
        }

    }
}
