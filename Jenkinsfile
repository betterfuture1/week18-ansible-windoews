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
                sh 'zip -r ansible-code.zip week18-ansible-windoews-x Jenkinsfile'
            }
        }

        stage('Store in JFrog') {
            steps {
                sh 'curl -uadmin:AP4KPM9fdPBKovDyeDco7NnkZZV -T ansible-code.zip "http://54.236.47.139:8081/artifactory/ansible-zip/"'
            }
        }

        stage('Deploy to Ansible Server') {
            agent {
                label 'ansible'
            }
            steps {
                sh 'curl -uadmin:AP4KPM9fdPBKovDyeDco7NnkZZV -O "http://54.236.47.139:8081/artifactory/ansible-zip/ansible-code.zip"'
            }
        }

        stage('Unzip the File') {
            agent {
                label 'ansible'
            }
            steps {
                sh 'unzip -o ansible-code.zip'
            }
        }

        /*
        stage('Copy to the Dest') {
            agent {
                label 'ansible'
            }
            steps {
                sh 'scp ansible-codes.zip ec2-user@34.201.153.232:/home/ec2-user/week18-ansible-dev/ansible-dev'
            }
        }
        */

        stage('Run Playbook') {
            steps {
                script {
                    dir ('ansibles-codes'){
                
                sh '/usr/local/bin/ansible-playbook -i /home/ec2-user/ansible-dev/workspace/Devops/ansible-pipeline/inventory.yml /home/ec2-user/ansible-dev/workspace/Devops/ansible-pipeline/code2.yml'
                 }
                }
            }
        }
    }
}

