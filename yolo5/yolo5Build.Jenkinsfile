pipeline {
    agent any

    stages {
        stage('ECR authentication and docker login') {

            steps {

                sh '''
                aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin 854171615125.dkr.ecr.us-east-2.amazonaws.com
                '''

            }

        }
        stage('Building') {

            steps {

                sh '''
                cd yolo5
                docker build -t swati-jenkins .
                '''

            }

        }



        stage('Push to ECR') {

            steps {

                sh '''
                docker tag swati-jenkins:latest 854171615125.dkr.ecr.us-east-2.amazonaws.com/swati-jenkins:0.0.${BUILD_NUMBER}
                docker push 854171615125.dkr.ecr.us-east-2.amazonaws.com/swati-jenkins:0.0.${BUILD_NUMBER}
                '''

            }

        }

        stage('Trigger Deploy') {
    steps {
        build job: 'Yolo5Deploy', wait: false, parameters: [
            string(name: '854171615125.dkr.ecr.us-east-2.amazonaws.com/swati-jenkins:0.0.18', value: "854171615125.dkr.ecr.us-east-2.amazonaws.com/swati-jenkins:0.0.${BUILD_NUMBER}")
        ]
    }
}

    }
}