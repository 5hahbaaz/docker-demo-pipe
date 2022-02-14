pipeline{
    agent any

    environment{
     //docker parameters   
        pathofdockerfile='.'                                //dockerfile path 
     //tagging the image   
        registry= 'hedgeness/oauth-server'                //registry
        version= ''                                       //version of the the image
    }

    stages{

        stage('git check') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [[$class: 'PathRestriction', excludedRegions: '', includedRegions: 'Jenkinsfile']], userRemoteConfigs: [[credentialsId: 'Github-Cred', url: 'https://github.com/hedgeness/oauth-server.git']]])
                  }
        }

        stage('build image') {
            steps {
                sh "docker build ${pathofdockerfile} -t ${registry}:${version}"
                  }
        }

        stage('login in to Dockerhub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'Dockerhub', passwordVariable: 'P', usernameVariable: 'U')]) {
                 sh "docker login -u ${U} -p ${P}"
                 //sh 'echo $P | docker login --username $U --password-stdin'
                    }
                  }
        }

        stage('Push to Dockerhub') {
            steps {
                 sh "docker push ${registry}:${version}"
                  }
        }

        stage('remove local image') {
            steps {
                 sh "docker rmi ${registry}:${version}"
                  }
        }      

    }
    post {
            always {
                sh 'docker logout'
            }
    }  

}
