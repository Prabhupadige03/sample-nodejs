pipeline {
    agent { label 'Prabhu' }   // Jenkins agent label

    environment {
        APP_DIR = "/home/ubuntu/sample-nodejs"
        APP_NAME = "sample-nodejs"   // PM2 process name (you can change if you want)
    }

    stages {
        stage('Checkout') {
            steps {
                dir("${APP_DIR}") {
                    git branch: 'main', url: 'https://github.com/Prabhupadige03/sample-nodejs.git'
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                dir("${APP_DIR}") {
                    sh 'npm install'
                }
            }
        }

        stage('Run Application with PM2') {
            steps {
                dir("${APP_DIR}") {
                    sh """
                        sudo -u ubuntu pm2 delete $APP_NAME || true
                        sudo -u ubuntu PORT=$PORT pm2 start ./bin/www --name $APP_NAME --update-env
                        sudo -u ubuntu pm2 save
                    """

                }
            }
        }

        stage('Verify') {
            steps {
                sh 'pm2 status $APP_NAME'
            }
        }
    }
}

