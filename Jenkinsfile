pipeline{
    agent{
        docker {
            image 'node:current-alpine3.13'
            args '-p 3000:3000 -p 5000:5000'
        }
    }
    environment {
        CI = 'true'
        HOME = '${WORKSPACE}'
    }
    stages{
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh 'chmod +rx scripts/test.sh'
                sh 'scripts/test.sh'
            }
        }
        stage('Delivery for development') {
            when {
                branch 'development'
            }
            steps {
                sh 'chmod +rx scripts/deliver-for-development.sh'
                sh 'chmod +rx script/kill.sh'
                sh 'scripts/deliver-for-development.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh 'scripts/kill.sh'
            }
        }
        stage('Deploy for production') {
            when {
                branch 'production'
            }
            steps {
                sh 'chmod +rx scripts/deploy-for-production.sh'
                sh 'chmod +rx scripts/kill.sh'
                sh 'scripts/deploy-for-production.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh 'scripts/kill.sh'
            }
        }
    }
}
    
