pipeline {
    agent any

    stages {

        stage('Install') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t backends .'
            }
        }

        stage('Network') {
            steps {
                sh 'docker network create auths-network || true'
            }
        }

        stage('Mongo') {
            steps {
                sh 'docker rm -f mongo || true && docker run -d --name mongo --network auths-network -v mongo_data:/data/db -p 27017:27017 mongo'
            }
        }

        stage('Backend') {
            steps {
                sh 'docker rm -f backend || true && docker run -d --name backend --network auths-network -e MONGO_URL=mongodb://mongo:27017/auth_demo -p 3000:3000 backends'
            }
        }
    }
}
