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
        
        stage('Deploy to Ansible Server and cp to ec2') {
            agent {
                label 'ansible'
            }
            steps {
                
                   
                    sh 'curl -uadmin:AP4KPM9fdPBKovDyeDco7NnkZZV -O  "http://3.85.1.71:8081/artifactory/ansible-zip/ansible-codes.zip"'

                    // Transfer the zip file to the Ansible server
                    sh 'scp ansible-codes.zip ec2-user@35.175.202.181:/home/ec2-user/'

                   
                }
            }
        stage('unzip the file'){
           agent {
             label 'ansible'
           }
         steps  {

                // Unzip the file on the Ansible server
                    sh 'ssh ec2-user@35.175.202.181 "unzip -o /home/ec2-user/ansible-codes.zip -d /home/ec2-user/ansible-dev/"'

                } 
            }        
          
        }
  

        

    }
