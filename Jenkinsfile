pipeline{
    agent any

    environment{
     //docker parameters   
        pathofdockerfile='.'                                //dockerfile path 
     //tagging the image   
        registry= '5hahbaaz/repo2'                //registry
        version= 'test'                                       //version of the the image
    }

    stages{

        stage('git check') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/dev']], extensions: [[$class: 'PathRestriction', excludedRegions: '', includedRegions: './Jenkinsfile']], userRemoteConfigs: [[credentialsId: 'cbe28b0a-4ac4-4b1f-b000-0eaaae2d5d76', url: 'https://github.com/5hahbaaz/docker-demo-pipe.git']]])
                  }
        } 
        
        stage('hello') {
            steps {
                powershell 'echo "hello"'
                  }
        } 
    }     
}
