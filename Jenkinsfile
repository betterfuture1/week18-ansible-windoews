pipeline {
    agent any
    environement
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
        
        stage('Deploy to Ansible Server') {
            steps {
                
                   
                    sh 'curl -uadmin:AP4KPM9fdPBKovDyeDco7NnkZZV -O "http://3.85.1.71:8081/artifactory/ansible-zip/"'

                    // Transfer the zip file to the Ansible server
                    sh 'scp ansible-codes.zip ec2-user@35.175.202.181:/home/ec2-user/'

                    // Unzip the file on the Ansible server
                    sh 'ssh ec2-user@<ANSIBLE_SERVER_IP> "unzip -o /home/ec2-user/ansible-codes.zip -d /home/ec2-user/ansible-dev/"'
                
                }
            }
    

  

        }

    }
