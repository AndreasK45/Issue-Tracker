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
                    echo 'password' | sudo -S apt update
                    sudo apt install python3-pip
                    pip3 install -r requirements.txt
                    cp ../../jenkins/workspace/DevOps-project/ansible/files/app/.env issue_tracker/.env
                    python3 manage.py test
                '''
            }
        }
    }
}