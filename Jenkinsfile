pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/dd-devops-18/jenkins-docker-demo.git',
                    branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t jenkins-demo:$BUILD_NUMBER .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                  docker rm -f demo || true
                  docker run -d -p 8081:80 --name demo jenkins-demo:$BUILD_NUMBER
                '''
            }
        }
    }
}
