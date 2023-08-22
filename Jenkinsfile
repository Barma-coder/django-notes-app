pipeline{
    agent any
    stages{
        stage("Code"){
            steps{
                echo "cloning the code"
                git url:"https://github.com/Barma-coder/django-notes-app.git",branch: "main"
            }
        }
        stage("build"){
            steps{
                echo "building the image"
                sh "docker build -t my-notes-app ."
            }
        }
        stage("Pushing code to DockerHub"){
            steps{
                echo "Pushing code to Docker Hube"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag my-notes-app ${env.dockerHubUser}/my-notes-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/my-notes-app:latest"
                }
            }
        }
        stage("deploy"){
            steps{
                echo "deploying the code"
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
