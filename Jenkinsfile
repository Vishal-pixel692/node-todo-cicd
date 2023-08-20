pipeline {
    agent { label 'dev' }
    
    stages {
        stage ('code'){
            steps {
                git url: 'https://github.com/Vishal-pixel692/node-todo-cicd.git', branch: 'master'
            }
            
        }
        stage ('Build & Test'){
            steps {
                sh 'docker build . -t vishalsd/node-todo-app-cicd:latest'
            }
            
        }
        stage ('Login & Push'){
            steps {
                echo 'Login & push'
                withCredentials([usernamePassword(credentialsId: 'Dockerhub', usernameVariable: 'dockerHubUser', passwordVariable: 'dockerhubPassword')]) {
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerhubPassword}"
                    sh "docker push vishalsd/node-todo-app-cicd:latest"
                }
                   
            }
            
        }
        stage ('deploy'){
            steps {
                sh 'docker-compose down && docker-compose up -d'
            }
            
        }
    }
}
