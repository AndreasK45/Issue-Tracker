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

        

        stage('Deploy django') {
            steps{
                sh '''
                   ansible-playbook -i ~/workspace/ansible-project/ansible/hosts.yml -l app01 --extra-vars "user_dir=/home/azureuser" ~/workspace/ansible-project/ansible/playbooks/application-gunicorn-ngix.yml 
                '''
            }
        }
    }
}