pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                // Clean and build the project using the specified Maven path
                sh '/usr/bin/mvn clean package'
            }
        }
        
        stage('Test') {
            steps {
                // Run tests using the specified Maven path
                sh '/usr/bin/mvn test'
            }
        }
    }
    
    post {
        always {
            // Actions to perform after the stages
            echo 'Pipeline finished.'
        }
        success {
            // Actions to perform if the pipeline succeeds
            echo 'Build and tests succeeded!'
        }
        failure {
            // Actions to perform if the pipeline fails
            echo 'Build or tests failed.'
        }
    }
}
