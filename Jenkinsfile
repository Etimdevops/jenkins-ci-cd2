pipeline {
    agent { label 'ansible' }  // Use the 'ansible' agent
    stages {
        stage('Checkout') {
            steps {
                dir('/home/ec2-user/jenkins-ci-cd2') {
                    git url: 'https://github.com/Etimdevops/jenkins-ci-cd2.git', branch: 'master'
                }
            }
        }
        stage('Build') {
            steps {
                dir('/home/ec2-user/jenkins-ci-cd2') {
                    ansiblePlaybook credentialsId: 'JenkinsAns', disableHostKeyChecking: true, installation: 'Ansible', inventory: 'hosts.ini', playbook: '01-build.yml'
                }
            }
        }
        stage('Test') {
            steps {
                dir('/home/ec2-user/jenkins-ci-cd2') {
                    ansiblePlaybook credentialsId: 'JenkinsAns', disableHostKeyChecking: true, installation: 'Ansible', inventory: 'hosts.ini', playbook: '02-test.yml'
                }
            }
        }
        stage('Deploy') {
            steps {
                dir('/home/ec2-user/jenkins-ci-cd2') {
                    ansiblePlaybook credentialsId: 'JenkinsAns', disableHostKeyChecking: true, installation: 'Ansible', inventory: 'hosts.ini', playbook: '03-deploy.yml'
                }
            }
        }
    }
}
