node{

   stage('SCM Checkout'){
       git branch: 'integration', url: 'https://github.com/shishirdevops/sapient.git'    
   }

	stage ("Build image") {
            steps {
                echo 'Starting to build docker image'
                script{
                    sh 'docker build -t shishir91/pandey:Int/${env.BUILD_ID} .'
                    
					}
            }
        }
  }
