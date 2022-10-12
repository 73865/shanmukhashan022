pipeline {
    agent any  
      stages {
        stage('Clone Repo') {
          steps {
            sh 'rm -rf shanmukhashan022'
            sh 'git clone https://github.com/73865/shanmukhashan022.git'
            }
        }

        stage('Build Docker Image') {
            steps {
              sh 'docker build -t pranaychander/nginx .'
              }
        }
        stage('Push Docker image') {
            environment {
                DOCKER_HUB_LOGIN = credentials('mvn')
            }
            steps {
                sh 'docker login --username=$DOCKER_HUB_LOGIN_USR --password=$DOCKER_HUB_LOGIN_PSW'
                sh    'docker push pranaychander/nginx'
            }
        }

        stage('Deploy to nginx') {
            steps {  
                sh    'docker run --name mynginx${BUILD_NUMBER} -d -p 80${BUILD_NUMBER}:80 pranaychander/nginx:latest'
            }
        }

        stage('Check WebApp Rechability') {
          steps {
          sh 'curl http://65.0.176.243:80${BUILD_NUMBER}'
          }
        }
      }
}
