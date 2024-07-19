pipeline {
    agent {
        label 'node3'
    }

    stages {
        stage('Build') {
            steps {
                echo 'build stage'
                sh '/opt/maven/bin/mvn package'
            }
        }
        
        stage('Test') {
            steps {
                echo 'Run tests'
                sh '/opt/maven/bin/mvn test'
            }
        }
    }
}
