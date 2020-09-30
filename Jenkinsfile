pipeline{
        agent any
        stages{
            stage('Build Image'){
                steps{
                    sh "sudo docker build -t chaperoo ."
                }
            }
            stage('Clean'){
                steps{
                    sh label: '', script: '''if [ "$(sudo docker ps -aq -f name=chaptodo)" ]; then
                        sudo docker rm -f chaptodo
                    fi'''
                    }
                }
            stage('Run Container'){
                steps{
                    sh "sudo docker run -d --name chaptodo -p 80:80 chaperoo"
                }
            }
        }    
}




pipeline{
                agent any
                environment {
                app_version = 'v1'
                rollback = 'false'
                }
                stages{
                stage('Build Image'){
        steps{
        script{
        if (env.rollback == 'false'){
        image = docker.build("[your-dockerhub-username]/chaperoo-frontend")
        }
}
}
}
stage('Tag & Push Image'){
steps{
script{
if (env.rollback == 'false'){
docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials'){
image.push("${env.app_version}")
}
}
}
}
}
stage('Deploy App'){
steps{
sh "docker-compose pull && docker-compose up -d"
}
}
}
}
