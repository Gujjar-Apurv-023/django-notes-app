@Library("shared") _
pipeline {
    agent any

    stages {
        stage("Hello"){
            steps{
                script{
                    hello()
                }
            }
        }

        stage("Code") {
            steps {
               script{
                 gitCheckout(
                    "https://github.com/Gujjar-Apurv-023/django-notes-app.git",
                    "dev"
                 )
                 echo "Code cloned successfully"
                }
            }
        }

        stage("Build") {
            steps {
                script{
                docker_build("notes-app","latest","apurv023")
                echo "Build successful"
                }
            }
        }

        stage("Push Image to Docker Hub") {
            steps {
                script{
                    docker_push("notes-app","latest","apurv023")
                    echo " image push on dockerhub successfully "
                }
            }
        }

        stage("Deploy") {
            steps {
                sh 'docker compose down && docker compose up -d'
                echo "Deployment successful"
                sh "docker ps"
                echo "successful visible running container"
                echo "done"
            }
        }
    }
}
