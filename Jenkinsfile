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
            when {
                branch 'main'
            }
            steps {
                script {
                    sh 'docker build -t nodemain:v1.0 .' 
                }
                
            }
        }

           stage('Docker build') { 
                when {
                branch 'dev'
            }
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
         stage('Deploy') { 
            when {
                branch 'main'
            }
            steps {
                sh 'docker run -d --expose 3001 -p 3001:3000 nodemain:v1.0' 
            }
    }
}
