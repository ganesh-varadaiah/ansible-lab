pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Who Am I') {
            steps {
                sh '''
                    whoami
                    pwd
                    ansible --version
                '''
            }
        }

        stage('Ansible Ping') {
            steps {
                sshagent(['ansible-key']) {
                    sh '''
                        ansible all -i inventory/hosts -m ping
                    '''
                }
            }
        }

        stage('Run Apache Playbook') {
            steps {
                sshagent(['ansible-key']) {
                    sh '''
                        ansible-playbook -i inventory/hosts apache.yml
                    '''
                }
            }
        }
    }
}
