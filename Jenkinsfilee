pipeline {
    agent any
    
    stages{
        stage("clone code"){
            steps {
                echo "clone the code into github"
                git url:"https://github.com/Shiba07s/notes-app.git", branch:"main"
            }
            
        }
        stage("build code"){
            steps {
                echo "build image"
                sh "docker build -t ashu-note-app ."
            }
            
        }
        stage("push to docker hub"){
            steps {
                 echo "Pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag ashu-note-app ${env.dockerHubUser}/ashu-note-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/ashu-note-app:latest"
                }
                 
            }
            
        }
        stage("deploy"){
            steps {
                echo "deploy"
                sh "docker-compose down && docker-compose up -d"
                
            }
            
        }
        
    }
}
