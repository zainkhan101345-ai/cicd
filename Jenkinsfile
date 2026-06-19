pipeline{
    agent any 
    environment {
        CONTAINER_NAME = 'nestjs-app'
        IMAGE_NAME = 'nestjs-image'
        EMAIL = 'zainkhan1980101@hotmail.com'
        PORT = "3000"
    }
    stages{
        stage('Clone repo'){
            steps{
                git branch:'main',url: 'https://github.com/zainkhan101345-ai/cicd.git'

            }
        }
        stage('Build Docker Image'){
            steps{
                sh 'docker build -t $IMAGE_NAME .'
            }
        }
        stage('Stop And Remove Previous Container'){
            steps{
                sh '''
                    docker stop -t $CONTAINER_NAME || true
                    docker rm -t $CONTAINER_NAME || true

                '''
                
            }
        }
          stage('Docker Run Container'){
            steps{
                sh '''
                 docker run -d \
                -p ${PORT}:${PORT} \
                --name $CONTAINER_NAME \
                $IMAGE_NAME
                '''
            }
        }

            stage('Send Email notifcation'){
            steps{
                emailext(
                      subject:"Next Js App Deployed Successfully on EC2 using Jenkins757dddddd12211234234dd2",
                    body:"Your NestJs App is deployed! http://http://13.48.56.138:${PORT}/",
                    to: "${EMAIL}"
                )
            }
        }

    }
}