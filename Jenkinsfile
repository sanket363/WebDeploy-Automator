pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                // Pull the Apache image
                sh 'docker pull httpd:latest'
            }
        }
        stage('Unit Test') {
            steps {
                // Run unit tests
                sh 'docker run --rm httpd:latest /bin/bash -c "cd /usr/local/apache2/htdocs && phpunit"'
                
            }
        }
        stage('Deploy') {
            steps {
                // Deploy to production
                sh 'docker run -d -p 80:80 httpd:latest'
            }
        }
    }
}
