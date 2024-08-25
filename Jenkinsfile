pipeline {
    agent { label 'ansible' }  // Use the 'ansible' agent
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Etimdevops/jenkins-ci-cd2.git', branch: 'master'
            }
        }
        stage('Build') {
            steps {
                ansiblePlaybook credentialsId: 'JenkinsAns', disableHostKeyChecking: true, installation: 'Ansible', inventory: '/home/ec2-user/jenkins-ci-cd2/hosts.ini', playbook: '/home/ec2-user/jenkins-ci-cd2/02-build.yml', vaultTmpPath: ''
            }
        }
        stage('Test') {
            steps {
                ansiblePlaybook credentialsId: 'JenkinsAns', disableHostKeyChecking: true, installation: 'Ansible', inventory: '/home/ec2-user/jenkins-ci-cd2/hosts.ini', playbook: '/home/ec2-user/jenkins-ci-cd2/03-test.yml', vaultTmpPath: ''
            }
        }
    }
}
