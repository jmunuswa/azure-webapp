pipeline 
{ 
	agent {label 'TestNode' }
	environment
	{
		def dockerHUBUser = 'jmunuswa'
		def registryCredential = 'dockerhub_id' 
		def seleniumTestJar = 'CapestonePrj1.jar'
	}
    stages 
	{ 
	
        stage('DownloadCode') 
		{ 

            steps 
			{
			
				echo "&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&[[[[[[RUN FROM : ${env.BRANCH_NAME}]]]]]]&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&"


					displayMessage("Download files from GitHub - Begin")

					git url: 'https://github.com/jmunuswa/azure-webapp.git',branch: 'master' 

				displayMessage("Download files from GitHub - End")
            }
 
        }
		
		stage('BuildCode') 
		{ 

            steps 
			{
			
				displayMessage("Build Docker image - Begin")
				
					sh "sudo docker build -t ${dockerHUBUser}/capstnprj1-${env.BRANCH_NAME} ."
				
				displayMessage("Build Docker image - End")
				
				displayMessage("Uplaod docker image to Dockerhub - Begin")
				 
					 withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) 
					 {
						sh "sudo docker login -u ${dockerHUBUser} -p ${dockerhubpwd}"
					 }
					 
					 sh "sudo docker push ${dockerHUBUser}/capstnprj1-${env.BRANCH_NAME}"
				 				 
				 displayMessage("Uplaod docker image to Dockerhub - End")
            }
 
        }
	 
    }           
 }
 
 
 void displayMessage(String argMessage) 
 {
    echo "*******************************************[[ ${argMessage} ]]****************************************************"
 }