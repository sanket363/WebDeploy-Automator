pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                // Build Docker image
                sh 'docker build -t my-apache-image .'
            }
        }
        stage('Unit Test') {
            steps {
                // Run unit tests
                sh 'docker run --rm my-apache-image /bin/bash -c "cd /var/www/html && phpunit"'
                
            }
        }
        stage('Deploy') {
            steps {
                // Deploy to production
                sh 'docker run -d -p 80:80 my-apache-image'
            }
        }
    }
}
