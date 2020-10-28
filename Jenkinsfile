pipeline { 
agent {label 'TestNode' }
	environment
	{
		def dockerHUBUser = 'jmunuswa'
		def registryCredential = 'dockerhub_id' 
	}
    stages { 
	
        stage('DownloadCode') { 

            steps {
			
				echo "&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&[[[[[[RUN FROM : ${env.BRANCH_NAME}]]]]]]&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&"
			
				
				displayMessage("Download files from GitHub - Begin")
			
                git url: 'https://github.com/jmunuswa/azure-webapp.git',branch: 'master' 
				
				displayMessage("Download files from GitHub - End")
            }
 
        }
		
		stage('BuildCode') { 

            steps {
			
				displayMessage("Build Docker image - Begin")
				
				sh "sudo docker build -t ${dockerHUBUser}/capstnprj1-${env.BRANCH_NAME} ."
				
				displayMessage("Build Docker image - End")
            }
 
        }
		
		
		stage('TestCode') { 

            steps {
                 
				 displayMessage("Run docker image and test using selenium - Begin")
				 
				 sh "sudo docker rm -f capstnprj1-${env.BRANCH_NAME} || true"
				 sh "sudo docker run -d -p 80:80 --name capstnprj1-${env.BRANCH_NAME}  ${dockerHUBUser}/capstnprj1-${env.BRANCH_NAME}"
				 sh "cp ./CapestonePrj1.jar  /home/ubuntu"
				 sh "java -jar CapestonePrj1.jar"
				 
				 displayMessage("Run docker image and test using selenium - End")
				 
				 displayMessage("Uplaod docker image to Dockerhub - Begin")
				 
				 withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) 
				 {
					sh "sudo docker login -u ${dockerHUBUser} -p ${dockerhubpwd}"
				 }
				 
				 sh "sudo docker push ${dockerHUBUser}/capstnprj1-${env.BRANCH_NAME}"
				 
				 
				 displayMessage("Uplaod docker image to Dockerhub - End")
				 
            }
 
        }
		
		
		stage('DeploytoPROD') { 

            steps {
			

				node('ProdNode')
				{
					 displayMessage("Pull docker image from Dockerhub - Begin")
					 
					 
					 
					 
					 displayMessage("Pull docker image from Dockerhub - End")
					 
					 displayMessage("Run docker image in PROD - Begin")
					 
					 
					 
					 
					 displayMessage("Run docker image in PROD - End")
				 }

                
            }
 
        }
		 
    }           
 }
 
 
 void displayMessage(String argMessage) {
    echo "*******************************************[ ${argMessage} ]****************************************************"
}