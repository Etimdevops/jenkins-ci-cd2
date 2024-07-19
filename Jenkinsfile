pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Build stage'
                sh '/opt/maven/bin/mvn clean package'
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

        // Adjust the path to your WAR file and Tomcat webapps directory accordingly
        sh 'cp /var/lib/jenkins/workspace/jenkins-ci-cd/target/WebAppCal-0.0.6.war ~/apache-tomcat-7.0.94/webapps/'

        // Restart Tomcat (if necessary)
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
