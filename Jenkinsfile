pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh '''
               sudo docker build -t 101275806917.dkr.ecr.ap-south-1.amazonaws.com/eks-ecr:$BUILD_NUMBER
               aws ecr get-login-password --region ap-south-1 | sudo docker login --username AWS --password-stdin 101275806917.dkr.ecr.ap-south-1.amazonaws.com
               sudo docker push 101275806917.dkr.ecr.ap-south-1.amazonaws.com/eks-ecr:$BUILD_NUMBER
               '''
            }
        }
        stage('eks deploy') {
            steps {
                sh '''
                cd k8s/
               kubectl apply -f .
               '''
            }
        }
    }
}