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
        
        stage('Deploy to Ansible Server ') {
            agent {
                label 'ansible'
            }
            steps {
                
                sh 'curl -uadmin:AP4KPM9fdPBKovDyeDco7NnkZZV -O  "http://35.153.231.68:8081/artifactory/ansible-zip/ansible-codes.zip/ansible-dev"'

                   
            }
        }
        stage ('copy to the dest'){
            steps {
                sh 'scp ansible-codes.zip ec2-user@54.160.65.37:/home/ec2-user/ansible-dev'
           }
        }

        stage('unzip the file'){
           agent {
             label 'ansible'
           }
         steps  {

                // Unzip the file on the Ansible server
                 sh 'ssh ec2-user@35.175.202.181 "unzip -o /home/ec2-user/ansible-codes.zip/ansible-dev -d /home/ec2-user/ansible-dev/"'

                } 
            }        
          
        }
    }
