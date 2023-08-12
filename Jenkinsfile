pipeline {
    agent any

    stages{
        stage('Build') {
            steps {
                git branch: 'main' , url: 'git@github.com:AndreasK45/Issue-Tracker.git' 
            }
        }

        stage('Test') {
            steps{
                sh '''
                    python3 -m venv myvenv
                    source myvenv/bin/activate
                    pip3 install -r requirements.txt
                    cp ~/workspace/ansible-project/ansible/files/app/.env issue_tracker/.env
                    python3 manage.py test
                '''
            }
        }

        stage('Deploy database') {
            steps{
                sh '''
                    ansible-galaxy install geerlingguy.postgresql
                '''
                sh '''
                    ansible-playbook -i ~/workspace/ansible-project/ansible/hosts.yml -l db01 ~/workspace/ansible-project/ansible/playbooks/postgres.yml 
                '''
            }
        }
    }
}