pipeline {
    agent any
    environment {
        AWS_ACCOUNT_ID="846265604884"
        AWS_DEFAULT_REGION="us-east-2"
        REPOSITORY_URI = "846265604884.dkr.ecr.us-east-2.amazonaws.com/bishopthesly"
    }


    stages{
       
        stage("Connecting to ECR"){
            step{
                script{
                    sh "aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin 846265604884.dkr.ecr.us-east-2.amazonaws.com"
                }
            }
       
        }  

        stage("Checking Git"){
            step{
               checkout scm
            }  
        }

        stage("Building Docker Image"){
            step{
                script{
                    sh "docker build -t bishopthesly ."
                }
            }
        }
        stage("Tagging and Pushing Image"){
            step{
                script{
                   sh "docker tag bishopthesly:latest 846265604884.dkr.ecr.us-east-2.amazonaws.com/bishopthesly:latest"
                   sh "docker push 846265604884.dkr.ecr.us-east-2.amazonaws.com/bishopthesly:latest"
                }
            }
        }
    }
}