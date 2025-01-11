pipeline {
    agent any
    environment {
        // Define variables, e.g., inventory and playbook
        INVENTORY_FILE = "inventory"
        PLAYBOOK_FILE = "playbook.yml"
    }
    stages {
        stage('Clone Repository') {
            steps {
                echo 'Cloning repository containing Ansible playbooks...'
                git branch: 'main', url: 'https://github.com/santhosh0811/PrometheusWithGrafana.git'
            }
        }
        stage('Install Ansible') {
            steps {
                echo 'Installing Ansible...'
                sh '''
                if ! command -v ansible >/dev/null 2>&1; then
                    sudo apt update
                    sudo apt install -y ansible
                fi
                '''
            }
        }
        stage('Check Ansible Syntax') {
            steps {
                echo 'Checking syntax of Ansible playbook...'
                sh "ansible-playbook --syntax-check ${PLAYBOOK_FILE}"
            }
        }
        stage('Run Ansible Playbook') {
            steps {
                echo 'Executing Ansible playbook...'
                sh "ansible-playbook -i ${INVENTORY_FILE} ${PLAYBOOK_FILE}"
            }
        }
    }
    post {
        success {
            echo 'Playbook execution succeeded!'
        }
        failure {
            echo 'Playbook execution failed!'
        }
    }
}
