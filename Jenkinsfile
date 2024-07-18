pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Example: Maven build
                sh '/opt/maven/bin/mvn package'
            }
        }
        
        stage('Test') {
            steps {
                // Run tests (adjust according to your testing framework)
                sh '/opt/maven/bin/mvn test'
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline succeeded! Deployment complete.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}

