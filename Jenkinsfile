pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Package Ansible Code') {
            steps {
                 sh ' zip -r ansible-code.zip week18-ansible-windoews-x Jenkinsfile '
                 
            }
        }
        stage('Store in jfrog') {
            steps {
                sh 'curl -uadmin:AP4KPM9fdPBKovDyeDco7NnkZZV -T ansible-code.zip "http://3.85.1.71:8081/artifactory/ansible-zip/"'  
            }
        }
        stage('Unzip Ansible Code') {
            steps {
                sh 'unzip -o ansible-code.zip -d /c/Users/fatou/devops-lab/week18-ansible-windoews'
            }
        }
        stage('Deploy to Ansible Server') {
            steps {
                sh 'scp ansible_code user@ansible-server:/home/ec2-user/ansible-dev'
                
            }
        }
    }
}
