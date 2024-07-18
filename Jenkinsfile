pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Build stage'
                sh '/opt/maven/bin/mvn package'
            }
        }
        
        stage('Test') {
            steps {
                echo 'Run tests'
                sh '/opt/maven/bin/mvn test'
            }
        }
        
        stage('Deploy') {
            steps {
                echo 'Deploying to Tomcat'

                // Assuming your Maven project builds a WAR file
                // Adjust the path to your WAR file accordingly
                sh 'cp /var/lib/jenkins/workspace/jenkins-ci-cd/target/WebAppCal-0.0.6.war ~/apache-tomcat-7.0.94/webapps'

                // Restart Tomcat (if necessary)
                // Replace 'tomcat8' with your actual Tomcat service name or path
                sh 'sudo systemctl restart tomcat8'
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
