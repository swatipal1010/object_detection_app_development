pipeline {
    agent any

    stages {
        stage('ECR authentication and Docker login') {

            steps {

                sh '''
                aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin 854171615125.dkr.ecr.us-east-2.amazonaws.com
                '''

            }

        }
        stage('Build') {

            steps {

                sh '''
                cd yolo5
                docker build -t swati-jenkins .
                '''

            }

        }



        stage('Pushing to ECR') {

            steps {

                sh '''
                docker tag swati-jenkins:latest 854171615125.dkr.ecr.us-east-2.amazonaws.com/swati-jenkins:0.0.${BUILD_NUMBER}
                docker push 854171615125.dkr.ecr.us-east-2.amazonaws.com/swati-jenkins:0.0.${BUILD_NUMBER}
                '''

            }

        }
    }
}