pipeline {

    agent any

    stages {

        stage('Check Python Installation') {
            steps {
                sh '''
                    python3 --version
                    pip3 --version
                '''
            }
        }

        stage('Create Virtual Environment') {
            steps {
                sh '''
                    python3 -m venv venv
                    . venv/bin/activate
                    python --version
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                    . venv/bin/activate
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Run Flask Application') {
            steps {
                sh '''
                    nohup venv/bin/python app.py > flask.log 2>&1 &
                '''
            }
        }

    }

    post {
        success {
            echo 'Flask application started successfully!'
        }

        failure {
            echo 'Pipeline execution failed!'
        }
    }
}
