pipeline {

  agent any
  tools {
    maven 'maven'
  }
  stages {
    stage('checkout') {
      steps {

        git branch: 'master', url: 'https://github.com/ShraddhaGithub123/demo.git'

      }
    }
    stage('Execute Maven') {
      steps {

        sh 'mvn clean install'
      }
    }

    stage('Pull Ansible playbook') {
      agent {
        label 'ans'
      }
      steps {
        git branch: 'master', url: 'https://github.com/ShraddhaGithub123/ansiblerepo'
      }
    }

    stage('Ansible Tomcat Deployment') {
      agent {
        label 'ans'
      }
      steps {
        ansiblePlaybook credentialsId: 'tomanscred',
          disableHostKeyChecking: true,
          installation: 'ansible',
          inventory: 'hosts',
          playbook: 'main.yaml'
      }
    }
  }
}
