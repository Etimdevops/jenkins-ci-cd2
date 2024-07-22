pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Build stage'
                sh '/opt/maven/bin/mvn package'
                
                // Stash the necessary files for deployment
                stash(name: 'Jenkinscicdfinal', includes: 'target/*.war')
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
                    // Corrected Tomcat download URL
                    def tomcatUrl = 'https://archive.apache.org/dist/tomcat/tomcat-8/v8.5.55/bin/apache-tomcat-8.5.55.tar.gz'
                    
                    // Download Tomcat using wget
                    sh "wget ${tomcatUrl} -O tomcat.tar.gz"
                    
                    // Extract Tomcat
                    sh 'mkdir -p /home/ec2-user/apache-tomcat-8.5.55'
                    sh 'tar -xzvf tomcat.tar.gz -C /home/ec2-user/apache-tomcat-8.5.55 --strip-components=1'
                    
                    // Create the target directory if it doesn't exist
                    sh 'mkdir -p /home/ec2-user/apache-tomcat-8.5.55/webapps'

                    // Remove existing WAR files (adjust path as necessary)
                    sh 'rm -f /home/ec2-user/apache-tomcat-8.5.55/webapps/*.war'

                    // Restore stashed WAR file (assuming it's stashed as 'Jenkinscicdfinal')
                    unstash 'Jenkinscicdfinal'

                    // Move the WAR file to the target directory
                    sh 'mv target/*.war /home/ec2-user/apache-tomcat-8.5.55/webapps/'

                    // Change permission for Tomcat startup script
                    sh 'chmod +x /home/ec2-user/apache-tomcat-8.5.55/bin/startup.sh'

                    // Start Tomcat
                    sh '/home/ec2-user/apache-tomcat-8.5.55/bin/startup.sh'
                }
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline succeeded! Deployment complete.'
            emailext(
                subject: "Jenkins Pipeline Succeeded",
                body: "The Jenkins pipeline has succeeded. Deployment is complete.",
                to: "etimvictordavid@gmail.com,etimvictordavid2@gmail.com"
            )
        }
        failure {
            echo 'Pipeline failed.'
            emailext(
                subject: "Jenkins Pipeline Failed",
                body: "The Jenkins pipeline has failed. Please check the logs for details.",
                to: "etimvictordavid@gmail.com,etimvictordavid2@gmail.com"
            )
        }
        always {
            echo 'Pipeline finished.'
        }
    }
}
