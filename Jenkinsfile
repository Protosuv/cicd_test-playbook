pipeline {
    agent { label 'ansible_docker' }

    stages {
        stage('Get from SCM') {
            steps {
                git 'https://github.com/Protosuv/cicd_test-playbook.git'
                sh 'ls -lah'
            }
        }
        stage('Install Java') {
            steps {
                sh 'ansible-galaxy install -r requirements.yml -p roles'
                ansiblePlaybook become: true, colorized: true, disableHostKeyChecking: true, inventory: 'inventory/prod.yml', playbook: 'site.yml'
            }
        }
        stage('Check version of Java') {
            steps {
                dir('/opt/jdk/openjdk-11+28_linux/bin/') {
                sh 'java -version'
                }
            }
        }
        }
    }