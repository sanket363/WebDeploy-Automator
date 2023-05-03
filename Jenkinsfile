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
                // Test the deployed application
                script {
                    def response = sh(script: "curl -I -s http://3.110.121.165:80 | head -n 1 | awk '{print $2}'", returnStdout: true).trim()
                    if (response == '200') {
                        echo "Application is running successfully with status code ${response}"
                    } else {
                        error "Application failed with status code ${response}"
                    }
                }
            }
        }
    }
}
