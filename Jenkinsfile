pipeline {
    agent any 
    tools {nodejs "node"}
    stages {
       
          stage('NPM install') { 
            steps {
                sh 'npm install'
            }
        }
        stage('Build') { 
            steps {
                sh 'npm build'
            }
        }
        stage('Test') { 
            steps {
                sh 'npm test' 
            }
        }
       stage('Docker build') { 
            steps {
                script {
                    sh 'docker build -t nodedev:v1.0 .' 
                }
                
            }
        }
        stage('Deploy') { 
            when {
                branch 'dev'
            }
            steps {
                sh 'docker run -d --expose 3000 -p 3000:3000 nodedev:v1.0' 
            }
          
        }
    }
}
