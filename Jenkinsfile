pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                // Pull the Todo app image
                sh 'docker pull snaket2628/todo:latest'
            }
        }
        stage('Stop Previous Container') {
            steps {
                script {
                    def containerID = sh(script: "docker ps -q --filter ancestor=snaket2628/todo:latest", returnStdout: true).trim()
                    if (containerID != "") {
                        sh "docker stop ${containerID}"
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                // Deploy the Todo app
                sh 'docker run -d -p 8000:8000 --name todo-app snaket2628/todo:latest'
            }
        }
        stage('Testing') {
            steps {
                // Test the deployed application
                script {
                    def response = sh(script: "curl -I -s http://3.110.121.165:8000 | head -n 1 | awk '{print \$2}'", returnStdout: true).trim()
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
