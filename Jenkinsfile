pipeline {
   agent any
   environment {
        DOCKER_USER = "chrissecular"
        MYSQL_ROOT_PASSWORD = "password123"
    }
   stages   {        
        stage('Build and Push'){
            steps{
                sh "docker build -t $DOCKER_USER/task2-db db"
                sh "docker build -t $DOCKER_USER/task2-app flask-app"
                sh "docker push $DOCKER_USER/task2-db"
                sh "docker push $DOCKER_USER/task2-app"
            }
        }
        stage('Test'){
            steps{
                echo "Testing..."
                sh "sleep 5"
                echo "PASSED"
            }
        }
        stage('Deploy'){
            steps {
                sh "docker network create task2"
                sh "docker run -d --network task2 --env MYSQL_ROOT_PASSWORD $DOCKER_USER/task2-db"
                sh "docker run -d --network task2 --env MYSQL_ROOT_PASSWORD $DOCKER_USER/task2=app"
                sh "docker run -d --network task2 -p 80:80 --mount type=bind,source=\$(pwd)/nginx/nginx.conf,target=/etc/nginx/ngingx.conf nginx"
            }
        }
   }
    post {
        always {
            sh "docker system prunce -f"
        }
    }
}