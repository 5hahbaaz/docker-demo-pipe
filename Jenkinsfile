pipeline {
    agent any

    stages {
        stage('git clone') {
            steps {
                git branch: 'dev', url: 'https://github.com/5hahbaaz/docker-demo-pipe.git'
                  }
        }

        stage('build docker image'){
            steps {                
                powershell "docker build 5hahbaaz/devimage:${BUILD_NUMBER} ." //$BUILD_NUMBER is being used as tag for the image
                  }
        }

        stage('log in to docker hub'){
           steps {
                // withCredentials([string(credentialsId: '599fc82b-b9f8-4c87-86c4-3fc985ad6c1d', variable: 'Password')]) {
                    
                // powershell "docker login -u 5hahbaaz -p ${Password}"        //use "" for groovy interpolation

                withCredentials([usernamePassword(credentialsId: 'DockerHub', passwordVariable: 'P', usernameVariable: 'U')]) {
                    powershell "docker login -u ${U} -p ${P}" 
                }
                
                powershell 'echo "login successful"' 
           }
        }

        stage('push to docker hub'){
           steps {
                powershell "docker push 5hahbaaz/devimage:${BUILD_NUMBER}"     
           }
        }
  
        stage('log out of docker hub'){
           steps {
                powershell 'docker logout'     
           }
        }
        stage('remove docker image from system'){
            steps {                
//                powershell "docker rmi 5hahbaaz/sampleimage:${BUILD_NUMBER}" //$BUILD_NUMBER is being used as tag for the image
                powershell "docker rmi 5hahbaaz/devimage:${BUILD_NUMBER}"
                  }
        }
    }
}    
