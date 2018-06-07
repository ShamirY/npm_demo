pipeline {
  agent any
  stages {
    stage('Build Demo App') {
      when {
        expression {
          params.REQUESTED_ACTION == 'Build'
        }

      }
      steps {
        sh '''npm install 
npm run build'''
      }
    }
    stage('Test') {
      when {
        expression {
          params.REQUESTED_ACTION == 'Build'
        }

      }
      steps {
        sh '''mkdir playbooks/files
cp nodejs-demoapp.zip playbooks/files/nodejs-demoapp.zip
ansible-playbook playbooks/deploy_dev.yml'''
      }
    }
    stage('DeployStage') {
      when {
        expression {
          params.REQUESTED_ACTION == 'Stage'
        }

      }
      steps {
        sh '''mkdir playbooks/files
cp nodejs-demoapp.zip playbooks/files/nodejs-demoapp.zip
ansible-playbook playbooks/deploy_dev.yml'''
      }
    }
  }
  parameters {
    choice(name: 'REQUESTED_ACTION', choices: '''Build
    Stage
''', description: 'Type of action to perform')
  }
}