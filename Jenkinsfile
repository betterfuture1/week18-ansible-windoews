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
                 sh ' zip -r ansible-codes.zip week18-ansible-windoews-x Jenkinsfile '
                 
            }
        }
        stage('Store in jfrog') {
            steps {
                sh 'curl -uadmin:AP4KPM9fdPBKovDyeDco7NnkZZV -T ansible-code.zip "http://35.153.231.68:8081/artifactory/ansible-zip/"'  
            }
        }
        
        stage('Deploy to Ansible Server ') {
            agent {
                label 'ansible'
            }
            steps {
                
                sh 'curl -uadmin:AP4KPM9fdPBKovDyeDco7NnkZZV -O  "http://35.153.231.68:8081/artifactory/ansible-zip/ansible-codes.zip/"'

                   
            }
        }
        
        stage('unzip the file'){
           agent {
             label 'ansible'
           }
         steps  {

                // Unzip the file on the Ansible server
                 sh 'unzip -o ansible-dev/ansible-codes.zip' 

                } 
            } 

        stage ('copy to the dest'){
            agent {
                label 'ansible'
            }
            steps {
                sh 'scp ansible-codes.zip ec2-user@34.201.153.232:/home/ec2-user/week18-ansible-dev/ansible-dev'
           }
        }
       
          
        }

    
    }
