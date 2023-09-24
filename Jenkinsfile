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
                    def currentBranch = env.BRANCH_NAME
                    if (currentBranch == 'main') {
                        sh 'docker build -t nodemain:v1.0 .' 
                    }else if (currentBranch == 'dev') {
                        sh 'docker build -t nodedev:v1.0 .' 
                    }   
                }        
            }
        }

        stage('Deploy') { 
            steps {
                script {
                      def currentBranch = env.BRANCH_NAME
                     if (currentBranch == 'main') {
                         sh 'docker run -d --expose 3000 -p 3000:3000 nodemain:v1.0' 
                    }else if (currentBranch == 'dev') {
                         sh 'docker run -d --expose 3001 -p 3001:3000 nodedev:v1.0' 
                    }   
                }      
            }
        }
    }
}
