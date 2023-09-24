pipeline {
    agent any 
    tools {nodejs "node"
          'org.jenkinsci.plugins.docker.commons.tools.DockerTool' 'docker'}
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
                    docker.build('nodedev:v1.0') 
                }
                
            }
        }
        stage('Deploy') { 
            steps {
                sh 'docker run -d --expose 3001 -p 3001:3000 nodedev:v1.0' 
            }
        }
    }
}
