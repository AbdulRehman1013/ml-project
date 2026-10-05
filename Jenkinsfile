pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // GitHub repository se code checkout karna
                git branch: 'main', url: 'https://github.com/AbdulRehman1013/ml-project.git'
            }
        }

        stage('Create Python Environment') {
            steps {
                // .dk naam se Python virtual environment banana
                sh 'python -m venv .dk'
            }
        }

        stage('Install Requirements') {
            steps {
                // .dk environment ke andar dependencies install karna
                sh '''
                    . .dk/bin/activate
                    cd Docker
                    pip install --no-cache-dir -r requirements.txt
                '''
            }
        }

        stage('Test Application') {
            steps {
                // Application syntax check
                sh '''
                    . .dk/bin/activate
                    cd Docker
                    python -c "import app; print('App syntax check passed!')"
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                // Docker image build karna
                dir('Docker') {
                    sh 'docker build -t docker-flask-app:latest .'
                }
            }
        }
    }

    post {
        success {
            echo 'Jenkins Pipeline completed successfully and Docker image built!'
        }
        failure {
            echo 'Jenkins Pipeline failed during execution.'
        }
    }
}