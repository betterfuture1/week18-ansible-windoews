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
                sh 'curl -uadmin:AP4KPM9fdPBKovDyeDco7NnkZZV -T ansible-code.zip "http://18.234.145.212:8081/artifactory/ansible-zip/"'
            }
        }

        stage('Deploy to Ansible Server') {
            agent {
                label 'ansible'
            }
            steps {
                sh 'curl -uadmin:AP4KPM9fdPBKovDyeDco7NnkZZV -O "http://18.234.145.212:8081/artifactory/ansible-zip/ansible-code.zip"'
            }
        }

        stage('Unzip the File') {
            agent {
                label 'ansible'
            }
            steps {
                sh 'unzip -o ansible-code.zip'
                dir ('ansible-code')
            }
        }

        
        /* stage('Copy to the Dest') {
            agent {
                label 'ansible'
            }
            steps {
                sh 'scp ansible-code ec2-user@54.237.32.132:/home/ec2-user//ansible-dev'
            }
        }*/
        
        

        stage('Run Playbook') {
            agent {
                label 'ansible'
            }
            steps {
                
                sh 'ansible-playbook -i home/ec2-user/ansible-dev/inventory.yml home/ec2-user/ansible-dev/workspace/Devops/ansible-pipeline/code-ansible/code2.yml'
                 
                
            }
        }
    }
}

