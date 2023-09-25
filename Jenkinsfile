pipeline {
    agent { label 'dev-agent' }
    stages {
        stage('code') {
            steps{
                git url:'https://github.com/Akshaynahar3/node-todo-cicd.git', branch: 'master'
            }
        }
        stage('build ') {
            steps{
                echo 'build'
                sh 'docker build . -t akshaynahar/node-todo-app:latest'
            }
        }
        stage('login & push') {
            steps{
                echo 'logging and pushing to docker'
                withCredentials([usernamePassword(credentialsId:'docker-hub',passwordVariable:'dockerpass',usernameVariable:'dockeruser')]){
                    sh "docker login -u ${env.dockeruser} -p ${env.dockerpass} && docker push ${env.dockeruser}/node-todo-app:latest"
                }
            }
        }
        stage('deploy') {
            steps{
                echo 'build'
                sh 'docker-compose down && docker-compose up -d'
            }
        }
    }
}
