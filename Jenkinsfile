pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'python3 -m venv .venv'
                sh '.venv/bin/pip install -r requirements.txt pytest'
            }
        }
        stage('Test') {
            steps {
                sh '.venv/bin/python -m pytest -v'
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                    nohup .venv/bin/python app.py > app.log 2>&1 &
                    sleep 3
                    curl -fsS http://localhost:5000/health
                '''
            }
        }
    }
}
