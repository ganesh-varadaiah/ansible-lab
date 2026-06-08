pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Ansible Ping') {
            steps {
                sh '''
                ansible all \
                -i inventory/hosts \
                -m ping
                '''
            }
        }

        stage('Run Apache Playbook') {
            steps {
                sh '''
                ansible-playbook \
                -i inventory/hosts \
                apache.yml
                '''
            }
        }
    }
}
