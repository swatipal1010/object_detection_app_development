pipeline {
    agent any
    
     # add the below line in the same level an `agent` and `stages`:
    parameters { string(name: '854171615125.dkr.ecr.us-east-2.amazonaws.com/swati-jenkins:0.0.19', defaultValue: '', description: '') }

    stages {
        stage('Deploy') {
            steps {
                sh '# kubectl apply -f ....'
            }
        }
    }
}
