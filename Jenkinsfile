pipeline{
    
    agent {label "vinod"}
    
    stages{ 
        stage("code"){
            steps{
                echo "this is cloning the code"
                git url: "https://github.com/VivekBelkhede/django-notes-app.git" , branch:"main"
                echo "code clonning successfully"
            }    
        }
        stage("build"){
             steps{
                echo "this is building the code"
                sh "whoami"
                sh "docker build -t notes-app:latest ."
            }   
        }
        stage("psuh to docker hub"){
             steps{
                echo "this is pushing the code to the dockerhub "
                withCredentials([usernamePassword(
                    credentialsId:"dockerHubcred",
                    usernameVariable:"dockerHubUser", 
                    passwordVariable:"dockerHubPass")]){
                sh "docker login -u${env.dockerHubUser} -p${env.dockerHubPass} "
                sh "docker image tag notes-app:latest vivekbelkhede/notes-app:latest"
                sh "docker push vivekbelkhede/notes-app:latest"
                }
        }    
    }
        stage("deploy"){
             steps{
                echo "this is deployning  the code"
                sh "docker compose up -d"
            }  
        }
    }    
}
