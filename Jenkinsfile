pipeline { 
agent {label 'TestNode' }
	environment
	{
		def dockerHUBUser = 'jmunuswa'
	}
    stages { 
	
        stage('DownloadCode') { 

            steps {
			
				echo "&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&[[[[[[RUN FROM : ${env.BRANCH_NAME}]]]]]]&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&"
			
				
				echo "****************************Download files from GitHub - Begin *********************************************"
			
                git url: 'https://github.com/jmunuswa/azure-webapp.git',branch: 'master' 
				
				echo "****************************Download files from GitHub - End *********************************************"
            }
 
        }
		
		stage('BuildCode') { 

            steps {
			
				echo "****************************Build Docker image - Begin *********************************************"
				
				sh "sudo docker build -t ${dockerHUBUser}/capstnprj1-${env.BRANCH_NAME} ."
				
				echo "****************************Build Docker image - End *********************************************"
            }
 
        }
		
		
		stage('TestCode') { 

            steps {
                 
				 echo "****************************Run docker image and test using selenium - Begin *********************************************"
				 
				 sh "sudo docker rm -f capstnprj1-${env.BRANCH_NAME} || true"
				 sh "sudo docker run -d -p 80:80 --name capstnprj1-${env.BRANCH_NAME}  ${dockerHUBUser}/capstnprj1-${env.BRANCH_NAME}"
				 sh "cp ./CapestonePrj1.jar  /home/ubuntu"
				 sh "java -jar CapestonePrj1.jar"
				 
				 echo "****************************Run docker image and test using selenium - End *********************************************"
				 
				 echo "****************************Uplaod docker image to Dockerhub - Begin *********************************************"
				 
				 
				 
				 
				 echo "****************************Uplaod docker image to Dockerhub - End *********************************************"
				 
            }
 
        }
		
		
		stage('DeploytoPROD') { 

            steps {
			


				 echo "****************************Pull docker image from Dockerhub - Begin *********************************************"
				 
				 
				 
				 
				 echo "****************************Pull docker image from Dockerhub - End *********************************************"
				 
				 echo "****************************Run docker image in PROD - Begin *********************************************"
				 
				 
				 
				 
				 echo "****************************Run docker image in PROD - End *********************************************"



                
            }
 
        }
		 
    }           
 }