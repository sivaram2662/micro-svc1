// pipeline {
//     agent any

//     stages {
//         stage('Build') {
//             steps {
//                 sh '''
//                sudo docker build -t 101275806917.dkr.ecr.ap-south-1.amazonaws.com/docker-ecr:$BUILD_NUMBER
//               aws ecr get-login-password --region ap-south-1 | sudo docker login --username AWS --password-stdin 101275806917.dkr.ecr.ap-south-1.amazonaws.com
//                sudo docker push 101275806917.dkr.ecr.ap-south-1.amazonaws.com/docker-ecr:BUILD_NUMBER
//                '''
//             }
//         }
//         // stage('eks deploy') {
//         //     steps {
//         //         sh '''
//         //    
//         //       kubectl apply -f .
//         //        '''
//         //     }
//         // }
//     }
// }



pipeline {
    agent any

    stages {
        stage('checkout') {
            steps {
                git branch: 'feature-docker', url: 'git@github.com:sivaram2662/micro-svc1.git'
               sh  'ls'    
            }
        }
         stage('login') {
            steps {
               sh "aws ecr get-login-password --region ap-south-1 | sudo docker login --username AWS --password-stdin 101275806917.dkr.ecr.ap-south-1.amazonaws.com"
            }
        }
        stage('build ') {
            steps {
               sh "sudo docker build -t 101275806917.dkr.ecr.ap-south-1.amazonaws.com/docker-ecr:latest ."
            }
        }
         stage('push') {
            steps {
               sh " sudo docker push 101275806917.dkr.ecr.ap-south-1.amazonaws.com/docker-ecr:latest"
        }
    }
       stage('eks deploy') {
            steps {
              sh '''
              kubectl create ns dev 
              helm upgrade -i static-dev static -n dev 
              '''
    }
}
}
}


