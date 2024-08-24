pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                script {
                    // Clean and build the project
                    sh 'mvn clean package'
                }
            }
        }
        
        stage('Test') {
            steps {
                script {
                    // Run tests
                    sh 'mvn test'
                }
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
