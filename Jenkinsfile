pipeline {
    agent any

    stages {

        stage('Build Backend Image') {
            steps {
                sh 'docker build -t backend-app backend'
            }
        }

        stage('Run Backend Containers') {
            steps {
                sh '''
                docker rm -f backend1 backend2 || true
                docker run -d -p 9001:9000 --name backend1 backend-app
                docker run -d -p 9002:9000 --name backend2 backend-app
                '''
            }
        }

        stage('Build NGINX Image') {
            steps {
                sh 'docker build -t nginx-lb nginx'
            }
        }

        stage('Run NGINX Container') {
            steps {
                sh '''
                docker rm -f nginx || true
                docker run -d -p 80:8081 --name nginx nginx-lb
                '''
            }
        }
    }
}
