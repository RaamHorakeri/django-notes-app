pipeline {
    agent any 
    
    stages{
        stage("Clone Code"){
            steps {
                echo "Cloning the code"
                git url:"https://github.com/LondheShubham153/django-notes-app.git", branch: "main"
            }
        }
        stage("Build"){
            steps {
                echo "Building the image"
                sh "docker build -t my-note-app ."
            }
        }
        stage("Push to Docker Hub"){
            steps {
                echo "Pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId: 'docker', passwordVariable: 'dockerpass', usernameVariable: 'docker')]){
                sh "docker tag my-note-app raam2023/my-note-app:latest"
                sh "docker login -u ${docker} -p ${dockerpass}"
                sh "docker push -t raam2023/my-note-app:latest"
                }
            }
        }
        stage("Deploy"){
            steps {
                echo "Deploying the container"
                sh "docker run -d -p 8000:8000 raam2023/my-note-app:latest"
                
            }
        }
    }
}
