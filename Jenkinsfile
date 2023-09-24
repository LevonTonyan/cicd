pipeline {
    agent any 
    stages {
          stage('Checkout SCM') { 
            steps {
                  git "https://github.com/LevonTonyan"
            }
        }
          stage('Tool install') { 
            steps {
                // 
            }
        }
        stage('Build') { 
            steps {
                sh 'npm install'
            }
        }
        stage('Test') { 
            steps {
                sh 'npm test' 
            }
        }
       stage('Docker build') { 
            steps {
                sh 'docker build -t nodedev:v1.0.' 
            }
        }
        stage('Deploy') { 
            steps {
                sh 'docker run -d --expose 3001 -p 3001:3000 nodedev:v1.0' 
            }
        }
    }
}
