pipeline {
    agent any

    stages {
        stage('Install') {
            steps {
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                echo 'Tests can be added here'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t combined-auth-app .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker rm -f combined-auth || true
                docker run -d -p 3000:3000 --name combined-auth combined-auth-app
                '''
            }
        }
    }
}
