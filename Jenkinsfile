pipeline {
    agent {
        label 'node2'
    }

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
            agent {
                label 'node2'
            }
            steps {
                echo 'Deploying to Tomcat'

                script {
                    // Download and install Apache Tomcat
                    def tomcatUrl = 'https://dlcdn.apache.org/tomcat/tomcat-8/v8.5.99/bin/apache-tomcat-8.5.99.tar.gz'
                    bat "powershell -command \"Invoke-WebRequest -Uri ${tomcatUrl} -OutFile tomcat.tar.gz\""
                    bat '7z x tomcat.tar.gz -otomcat'

                    // Create the target directory if it doesn't exist
                    bat 'mkdir C:\\Users\\ec2-user\\apache-tomcat-8.5.99\\webapps'

                    // Remove existing WAR files (adjust path as necessary)
                    bat 'del /Q C:\\Users\\ec2-user\\apache-tomcat-8.5.99\\webapps\\*.war'

                    // Restore stashed WAR file (assuming it's stashed as 'Jenkinscicdfinal')
                    unstash "Jenkinscicdfinal"

                    // Move the WAR file to the target directory
                    bat 'move target\\*.war C:\\Users\\ec2-user\\apache-tomcat-8.5.99\\webapps'

                    // Restart Tomcat (adjust path as necessary)
                    bat 'C:\\Users\\ec2-user\\apache-tomcat-8.5.99\\bin\\startup.bat'
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
