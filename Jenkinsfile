pipeline{
    
    agent any;
    stages{
        
        stage("Code CLone"){
            steps{
                git url: "https://github.com/harshkhairajani/two-tier-flask-app.git", branch: "master"
            }
        }
        
        stage("Build"){
            steps{
                sh "docker build -t my-app ."
            }
        }
        
        stage("Test"){
            steps{
                echo "This is clone"
            }
        }
        
        stage("Docker Hub Push"){
            steps{
                withCredentials([usernamePassword(
                    credentialsId:"DockerHubJenkins",
                    passwordVariable: "dockerhubpass",
                    usernameVariable: "dockerhubuser"
                )]){
                    
                    sh "docker login -u ${env.dockerhubuser} -p ${env.dockerhubpass}"
                    sh "docker image tag my-app ${env.dockerhubuser}/my-app"
                    sh "docker push ${env.dockerhubuser}/my-app"
                }
            }
        }
        
        stage("Deploy"){
            steps{
                sh "docker compose up -d --build flask-app"
            }
        }
        
    }
}
