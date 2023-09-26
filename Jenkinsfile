pipeline
{   agent any
    stages{
        stage('Code')
        {
            steps{
                git url: 'https://github.com/Akshaynahar3/node-todo-cicd.git', branch: 'master'
            }
        }
        stage('Build')
        {
            steps{
               sh "docker build . -t node-cicd-app"
            }
        }
        stage('Push')
        {
            steps{
                withCredentials([usernamePassword(credentialsId:'dockerhub',usernameVariable:'dockeruser',passwordVariable:'dockerpass')]){
                    sh "docker login -u ${env.dockeruser} -p ${env.dockerpass}"
                    sh "docker tag node-cicd-app ${env.dockeruser}/node-cicd-app:latest"
                    sh "docker push ${env.dockeruser}/node-cicd-app:latest"
                }
            }
        }
        stage('Deploy')
        {
            steps{
               sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
