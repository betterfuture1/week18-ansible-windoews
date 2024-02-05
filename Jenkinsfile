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
                sh 'zip -r ansible-codes.zip week18-ansible-windoews-x Jenkinsfile'
            }
        }

        stage('Store in JFrog') {
            steps {
                sh 'curl -uadmin:AP4KPM9fdPBKovDyeDco7NnkZZV -T ansible-codes.zip "http://100.24.238.101:8081/artifactory/ansible-zip/"'
            }
        }

        stage('Deploy to Ansible Server') {
            agent {
                label 'ansible'
            }
            steps {
                sh 'curl -uadmin:AP4KPM9fdPBKovDyeDco7NnkZZV -O "http://100.24.238.101:8081/artifactory/ansible-zip/ansible-codes.zip"'
            }
        }

        stage('Unzip the File am play playbook') {
            agent {
                label 'ansible'
            }
            steps {
                script {
                    // Unzip ansible-codes.zip
                    sh 'unzip -o ansible-codes.zip'
                    // Run ansible-playbook from the correct directory
                    dir('ansible-code') {
                        sh 'ansible-playbook -i home/ec2-user/ansible-dev/inventory.yml  /home/ec2-user/ansible-dev/code2.yml'
                   }
                }
            }

        }
        stage('play the cron job') {
            agent {
                label 'ansible'
            }
            steps {
                
                        sh 'ansible-playbook -i home/ec2-user/ansible-dev/inventory.yml  /home/ec2-user/ansible-dev/cron-update.yml'
                   }
                }
            }

    

