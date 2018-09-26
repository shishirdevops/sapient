node{
     
     stage('login to swarm node')
     
          {
     sh "ssh jenkins@swarmnode"
          }

     
stage('Pull Docker Image'){
     withCredentials([string(credentialsId: 'shishir91', variable: 'dockerHubPwd')]) {
        sh "docker login -u shishir91 -p ${dockerHubPwd}"
     }
     sh "docker pull shishir91/pandey:${artifact}"
   }

   stage ('Approval') {
            //steps {
                echo 'Kindly, confirm to proceed.'
                script {    
                  def deploy_prod_verify = input id: 'Deploy', message: 'Proceed?', ok: 'Deploy!'
            }
        //}
    }
        
   stage('Remove Old Containers'){
   // sshagent(['dev-server']) {
     try{
        def dockerRM = 'docker rm -f my-app'
        sh "${dockerRM}"
      }
      catch(error){
      }
    //}
  }
   stage('Run Container on Server'){
     def dockerRun = "docker run -p 8080:8080 -d --name my-app shishir91/pandey:${artifact}"
     sh "${dockerRun}"
     }
   
}
