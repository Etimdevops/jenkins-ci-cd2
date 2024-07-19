pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Build stage'
                bat 'mvn clean package'
            }
        }
        
        stage('Test') {
            steps {
                echo 'Run tests'
                bat 'mvn test'
            }
        }
        
        stage('Deploy') {
            agent {
                label 'node1'
            }
            steps {
                echo 'Deploying to Tomcat'

                script {
                    // Define the URL to download Apache Tomcat
                    def tomcatUrl = 'https://dlcdn.apache.org/tomcat/tomcat-8/v8.5.99/bin/apache-tomcat-8.5.99.tar.gz'

                    // Download and install Apache Tomcat
                    sh "wget -q -O tomcat.tar.gz ${tomcatUrl}"
                    sh "sudo tar -xzf tomcat.tar.gz -C /opt"

                    // Additional deployment steps
                    sh "mkdir -p /home/ec2-user/apache-tomcat-8.5.99/webapps"
                    sh "sudo mv target/*.war /home/ec2-user/apache-tomcat-8.5.99/webapps/"
                    sh "sudo /opt/apache-tomcat-8.5.99/bin/startup.sh"
                }
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
