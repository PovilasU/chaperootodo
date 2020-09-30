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
                         image = docker.build("povilasu/chaperoo-frontend")
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
        
        stage('Runs Containers'){
                steps{
                        sh "sudo docker-compose pull && docker-compose up -d"
                }
             }
        }
}
