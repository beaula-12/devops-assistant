pipeline {
    agent any

    environment {
        VENV = "venv"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Python') {
            steps {
                sh '''
                apt-get update
                apt-get install -y python3 python3-pip python3-venv
                '''
            }
        }

        stage('Setup Python') {
            steps {
                sh '''
                python3 --version
                python3 -m venv $VENV
                . $VENV/bin/activate
                pip install --upgrade pip
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                . $VENV/bin/activate
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                . $VENV/bin/activate
                pytest
                '''
            }
        }
    }

    post {
        always {
            echo 'Build Finished'
        }
        success {
            echo 'Build Passed ✅'
        }
        failure {
            echo 'Build Failed ❌'
        }
    }
}
