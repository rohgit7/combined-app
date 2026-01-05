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
                bat 'docker build -t backend-image .'
            }
        }

        stage('Network') {
            steps {
                bat 'docker network create auths-networks || exit 0'
            }
        }

        stage('Mongo') {
            steps {
                bat 'docker run -d --name mongo_container --network auths-networks -v mongo_data:/data/db -p 27017:27017 mongo'
            }
        }

        stage('Backend') {
            steps {
                bat 'docker run -d --name backend --network auths-networks -e MONGO_URL=mongodb://mongo_container:27017/auth_demo -p 3000:3000 backend-image'
            }
        }
    }
}
