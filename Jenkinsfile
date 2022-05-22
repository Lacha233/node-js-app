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
      parallel {
        stage('Build/Linux') {
          steps {
            sh '''echo \'Build successfull for Linux platform.\'
'''
          }
        }

        stage('Build/Windows') {
          steps {
            sh '''echo \'Build successful for Windows platform.\'
'''
          }
        }

      }
    }

  }
  environment {
    ANSIBLE_CONFIG = '/opt/kickstart-ansible/ansible.cfg'
  }
}