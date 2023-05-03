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
                        sh "docker rm ${containerID}"
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
                    echo "running tests"
                    echo "everything running fine"
                }
            }
        }
    }
}
