pipeline {
    agent any

    stages {

        stage('Install') {
            steps {
                bat 'npm install'
            }
        }

        stage('Build Image') {
            steps {
                bat 'docker build -t backends .'
            }
        }

        stage('Network') {
            steps {
                bat 'docker network create auths-network || exit 0'
            }
        }

        stage('Mongo') {
            steps {
                bat 'docker rm -f mongo || exit 0 && docker run -d --name mongo --network auths-network -v mongo_data:/data/db -p 27017:27017 mongo'
            }
        }

        stage('Backend') {
            steps {
                bat 'docker rm -f backend || exit 0 && docker run -d --name backend --network auths-network -e MONGO_URL=mongodb://mongo:27017/auth_demo -p 3000:3000 backends'
            }
        }
    }
}
