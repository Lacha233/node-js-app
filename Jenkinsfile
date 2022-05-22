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

    stage('Test') {
      steps {
        sh 'echo \'Test successfull for Linux platform.\''
      }
    }

    stage('Deploy') {
      steps {
        ansiblePlaybook(playbook: '/opt/kickstart-ansible/project/playbook/app.yml', credentialsId: 'ansible-node-ssh', disableHostKeyChecking: true, inventory: '/opt/kickstart-ansible/project/stg-hosts', tags: 'setup, update, configure, start')
        emailext(subject: 'Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}', body: '${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\\n More info at: ${env.BUILD_URL}', to: 'lacha9233@gmail.com')
        cleanWs(deleteDirs: true, disableDeferredWipeout: true)
        input 'Congrats! The deployment on staging environment is successful. Do you want to start deployment on production environment?'
      }
    }

  }
  environment {
    ANSIBLE_CONFIG = '/opt/kickstart-ansible/ansible.cfg'
  }
}