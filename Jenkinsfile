pipeline {
    
    agent any
    stages {
stage ('Merge pull request') {
    steps { 
	
	try{
        withCredentials([usernamePassword(credentialsId: 'credential-value', usernameVariable: 'ACCESS_TOKEN_USERNAME', passwordVariable: 'ACCESS_TOKEN_PASSWORD',)]) {
            sh "curl -X PUT -d '{\"commit_title\": \"Merge pull request\"}'  https://github.com/shishirdevops/sapient/pull/2/merge?access_token=$ACCESS_TOKEN_PASSWORD"
        }
    } catch(error){
      } }
}

stage('Build Docker Image'){
    steps{
	try{
     sh "docker build -t shishir91/pandey:${env.BUILD_ID} ."
    } catch(error){
      } } }
  
  stage('Push Docker Image'){
  steps{
     withCredentials([string(credentialsId: 'shishir91', variable: 'dockerHubPwd')]) {
        sh "docker login -u shishir91 -p ${dockerHubPwd}"
     }
  try{   sh "docker push shishir91/pandey:${env.BUILD_ID}"
} catch(error){
      }} }


stage('login to swarm node')
     
          { steps {
     sh "ssh jenkins@swarmnode"
}  }

stage('Pull Docker Image'){
     withCredentials([string(credentialsId: 'shishir91', variable: 'dockerHubPwd')]) {
        sh "docker login -u shishir91 -p ${dockerHubPwd}"
     }
     sh "docker pull shishir91/pandey:${env.BUILD_IDt}"
}
  
   stage ('Approval') {
       steps{
                   echo 'Kindly, confirm to proceed.'
                script {    
                  def deploy_prod_verify = input id: 'Deploy', message: 'Proceed?', ok: 'Deploy!'
            }
       }
    }
        
   stage('Remove Old Containers'){
       steps{
     try{
        def dockerRM = 'docker rm -f my-app'
        sh "${dockerRM}"
      }
      catch(error){
      }
       }
  }
   stage('Run Container on Server'){
       steps{ def dockerRun = "docker run -p 5098:8080 -d --name my-app shishir91/pandey:${env.BUILD_ID}"
     sh "${dockerRun}"
            } }
stage('test run of container')
{
    steps {
sh"docker ps"
    }
}
   
}
}
