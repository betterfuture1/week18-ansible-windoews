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
                 sh 'zip -r ansible_code.zip -i /home/ec2-user/ansible-dev/*'
            }
        }
        stage('Store in jfrog') {
            steps {
                sh 'curl -uadmin:AP4KPM9fdPBKovDyeDco7NnkZZV -T /home/ec2-user/ansible-dev "http://35.153.52.148:8081/artifactory/ansible-zip//home/ec2-user/ansible"'  
            }
        }
        stage('Unzip Ansible Code') {
            steps {
                sh 'unzip -o ansible_code.zip -d /home/ec2-user/ansible-dev'
            }
        }
        stage('Deploy to Ansible Server') {
            steps {
                sh 'scp ansible_code user@ansible-server:/home/ec2-user/ansible-dev'
                
            }
        }
    }
}
