pipeline{
    agent any
    environment{
        DOCKER_TAG = getDockerTag()
     }
    stages{
       stage("git checkout"){
           steps{
               git 'https://github.com/manojsamy/sampledemo'
               }
             }
       stage("docker build"){
            steps{
                sh "docker build . -t manojimages/sampletypes:$(DOCKER_TAG)"
                }
             }  
       stage("pushing the image"){
            steps{
                withCredentials([string(credentialsId: 'dockerpwd', variable: 'dockerpsd')]) {
                sh "docker login -u manojimages -p $(dockerpsd)"
                sh "docker push manojimages/sampletypes:$(DOCKER_TAG)"
                }
             }   
          }        
       }   
    }
def getDockerTag(){
    def tag = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}    
