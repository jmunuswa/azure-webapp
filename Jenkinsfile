pipeline { 
agent {label 'TestNode' }
	environment
	{
		def dockerHUBUser = 'jmunuswa'
		def registryCredential = 'dockerhub_id' 
		def seleniumTestJar = 'CapestonePrj1.jar'
		def argServer = 'http://3.14.1.246/index.htm'
		def argDriver = '/home/ubuntu/chromedriver'
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
            }
 
        }
		
		
		stage('TestCode') 
		{ 

            steps 
			{
                 
				 displayMessage("Run docker image and test using selenium - Begin")
				 
					 sh "sudo docker rm -f capstnprj1-${env.BRANCH_NAME} || true"
					 sh "sudo docker run -d -p 80:80 --name capstnprj1-${env.BRANCH_NAME}  ${dockerHUBUser}/capstnprj1-${env.BRANCH_NAME}"
					 sh "cp ./CapestonePrj1.jar  /home/ubuntu"
					 sh "java -jar ${seleniumTestJar} ${argServer} ${argDriver}"
				 
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
		
		
		stage('DeploytoPROD') 
		{ 
			when 
			{
				branch "master"
			}

            steps 
			{
			
			
				node('ProdNode')
				{
				

					 
					 displayMessage("Run docker image in PROD - Begin")
					 
					 	sh "sudo docker rm -f capstnprj1-${env.BRANCH_NAME} || true"
						sh "sudo docker image pull ${dockerHUBUser}/capstnprj1-${env.BRANCH_NAME}"
						sh "sudo docker run -d -p 80:80 --name capstnprj1-${env.BRANCH_NAME}  ${dockerHUBUser}/capstnprj1-${env.BRANCH_NAME}"
					 
					 displayMessage("Run docker image in PROD - End")
				}

                
            }
 
        }
		 
    }           
 }
 
 
 void displayMessage(String argMessage) 
 {
    echo "*******************************************[[ ${argMessage} ]]****************************************************"
 }