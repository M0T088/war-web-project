String maven = "maven:3.6.3-adoptopenjdk-14"
pipeline {
    agent any
    stages {
        stage('docker-compose up') {
          steps {
            sh 'docker-compose up -d'
          }
        }
        stage('war File') {
            agent {
                docker {
                    image 'maven'
                    args '--network tomcat_moto_net'
                }
            }
            steps {
                    sh 'mvn package'
                    }
                }
        stage('Deploy War File') {
            steps {
				ansiblePlaybook colorized: true, installation: 'ansible2', playbook: 'dockertest.yml', disableHostKeyChecking: true
            }
        }
    }
}
