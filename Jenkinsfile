pipeline{
    agent{
        docker {
            image 'node:6-alpine'
            args '-p 3000:3000 -p 5000:5000'
        }
    }
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                sh 'sudo chown -R `whoami` /usr/local'
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/script/teste.sh'
            }
        }
    }
    
}