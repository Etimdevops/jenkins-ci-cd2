pipeline {
    agent any
    
    environment {
        JAVA_HOME = '/usr/lib/jvm/java-11-openjdk-11.0.23.0.9-2.el7_9.x86_64'
        MAVEN_HOME = '/usr/share/maven'  // Update this path if your Maven installation is in a different location
    }
    
    stages {
        stage('Build') {
            steps {
                // Clean and build the project using the specified Maven path
                sh "${env.MAVEN_HOME}/bin/mvn clean package"
            }
        }
        
        stage('Test') {
            steps {
                // Run tests using the specified Maven path
                sh "${env.MAVEN_HOME}/bin/mvn test"
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
