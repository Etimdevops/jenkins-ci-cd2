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
            agent {
                label 'node3' // Replace with the label of the node you want to deploy to
            }
            steps {
                echo 'Deploying to Tomcat'

                script {
                    // Download and install Apache Tomcat using wget
                    def tomcatUrl = 'https://dlcdn.apache.org/tomcat/tomcat-8/v8.5.99/bin/apache-tomcat-8.5.99.tar.gz'
                    sh "wget ${tomcatUrl} -O tomcat.tar.gz"  // Use wget command to download Tomcat

                    sh 'tar -xzvf tomcat.tar.gz -C tomcat'  // Extract Tomcat

                    // Create the target directory if it doesn't exist
                    sh 'mkdir -p /home/ec2-user/apache-tomcat-8.5.99/webapps'

                    // Remove existing WAR files (adjust path as necessary)
                    sh 'rm -f /home/ec2-user/apache-tomcat-8.5.99/webapps/*.war'

                    // Restore stashed WAR file (assuming it's stashed as 'Jenkinscicdfinal')
                    unstash 'Jenkinscicdfinal'

                    // Move the WAR file to the target directory
                    sh 'mv target/*.war /home/ec2-user/apache-tomcat-8.5.99/webapps'

                    // Start Tomcat (adjust path as necessary)
                    sh '/home/ec2-user/apache-tomcat-8.5.99/bin/startup.sh'
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
