pipeline{
    agent any
    
    stages{
        stage("Code"){
            steps{
                git url: "https://github.com/Karan90988/node-todo-cicd.git", branch: "master"
            }
        }
        stage("Building Docker-Image"){
            steps{
                sh "docker build . -t karan90988/node-todo-application"
            }
        }
        stage("Pushing Docker Image to DockerHub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerhub", usernameVariable: "dockerUsername", passwordVariable: "dockerPassword")]){
                    sh "docker login -u ${env.dockerUsername} -p ${env.dockerPassword}"
                    sh "docker push karan90988/node-todo-application:latest"
                }
            }
        }
        stage("Test"){
            steps{
                echo "Testing Stage"
            }
        }
        stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        } 
    }
}
