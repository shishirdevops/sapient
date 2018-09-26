pipeline{
	stages{
   stage('SCM Checkout'){
       git branch: 'integration', url: 'https://github.com/shishirdevops/sapient.git'    
                        }

	stage ('Build image') {
            steps {
                echo 'Starting to build docker image'
                script{
                    sh 'sudo usermod -a -G dockerroot jenkins'
                    def customImage = docker.build("my-image:${env.BUILD_ID}")
                }
            }        }
  }
}
