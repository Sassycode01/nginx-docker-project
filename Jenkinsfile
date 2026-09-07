pipeline {
    agent any
    
    stages {
        
       stage('clone') {
           steps {
              checkout scm
           }
       }

       stage('Build Docker Image') {
           steps {
               sh 'docker build -t sassy2031/mynginx:latest .'
           }
       }

       stage('Docker Compose') {
           steps {
               sh 'docker compose down || true'
               sh 'docker compose up -d'
           }
       }

       stage('verify') {
           steps {
               sh 'docker ps'
               sh 'curl -f http://localhost:8080'
           }
       }
    }
}        
