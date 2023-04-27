pipeline {
    agent { label 'dev-agent' }
    
    stages{
        stage('Code'){
            steps {
                git url: 'https://github.com/biswojit01/node-todo-cicd.git', branch: 'master'
            }
        }
        stage('Build and Test'){
            steps {
              sh 'docker build . -t biswojit01/node-todo-app-cicd:latest'
            }
        }
        stage('Login and push Image'){
            steps {
                echo "Login into dockerhub and pushing image"
                withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                    sh "docker push biswojit01/node-todo-app-cicd:latest "
                }

            }
        }
        stage('Deploy'){
            steps {
                sh 'docker-compose down && docker-compose up -d'
            }
        }
        
    }
}
