pipeline {
    agent {
        docker {
            image 'docker:24.0.5'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    stages {

        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/YOURNAME/jenkins-docker-demo.git',
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
