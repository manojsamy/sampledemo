pipeline{
    agent any
    environment{
        Docker_tag = getDockerTag()
     }
    stages{
       stage("git checkout"){
           steps{
               git 'https://github.com/manojsamy/sampledemo'
               }
             }
       stage("docker build"){
            steps{
                sh "docker build . -t manojimages/sampletypes:$(Docker_tag)"
                }
             }  
       stage("pushing the image"){
            steps{
                withCredentials([string(credentialsId: 'dockerpwd', variable: 'dockerpsd')]) {
                sh "docker login -u manojimages -p $(dockerpsd)"
                sh "docker push manojimages/sampletypes:$(Docker_tag)"
                }
             }   
          }        
       }   
    }
def getDockerTag(){
    def tag = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}    
