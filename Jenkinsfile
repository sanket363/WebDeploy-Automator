pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                // Pull the Apache image
                sh 'docker pull httpd:latest'
            }
        }
        stage('Deploy') {
            steps {
                // Deploy to production
                sh 'docker run -d -p 80:80 httpd:latest'
            }
        }
        stage('Testing') {
            steps {
                // Deploy to production
                sh 'curl -I -s http://3.110.121.165:80 | head -n 1 | awk '{print $2}''
            }
        }
    }
}
