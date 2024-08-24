pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Etimdevops/jenkins-ci-cd2.git', branch: 'master'
            }
        }
        stage('Build and Test') {
            steps {
                ansiblePlaybook credentialsId: 'JenkinsAns', disableHostKeyChecking: true, installation: 'Ansible', inventory: '/home/ec2-user/jenkins-ci-cd2/hosts.ini', playbook: '/home/ec2-user/jenkins-ci-cd2/02-buildtest.yml', vaultTmpPath: ''
            }
        }
    }
}
