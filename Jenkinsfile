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
                script {
                    dir ('week18-ansible-windoewszx')
                }
                 sh ' zip -r ansible_code.zip  -x Jenkinsfile
                 '
            }
        }
        stage('Store in jfrog') {
            steps {
                sh 'curl -uadmin:AP4KPM9fdPBKovDyeDco7NnkZZV -T ansible_code.zip "http://35.153.52.148:8081/artifactory/ansible-zip/"'  
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
