pipeline {
  agent {
    node {
      label 'slave'
    }

  }
  stages {
    stage('Prepare') {
      steps {
        sh 'easy_install pip'
        sh 'pip install ansible==2.8.2'
      }
    }

    stage('Build') {
      steps {
        sh '''echo \'Build successfull for Linux platform.\'
'''
      }
    }

  }
  environment {
    ANSIBLE_CONFIG = '/opt/kickstart-ansible/ansible.cfg'
  }
}