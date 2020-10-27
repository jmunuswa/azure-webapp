pipeline { 
agent {label 'TestNode' }
	environment
	{
		def dockerHUBUser = 'jmunuswa'
	}
    stages { 
	
        stage('DownloadCode') { 

            steps {
                git url: 'https://github.com/jmunuswa/azure-webapp.git',branch: 'master' 
            }
 
        }
		
		stage('BuildCode') { 

            steps {
			
				sh "sudo docker build -t ${dockerHUBUser}/capstnprj1-${env.BRANCH_NAME} ."
            }
 
        }
		
		
		stage('TestCode') { 

            steps {
                 
				 sh "sudo docker rm -f capstnprj1-${env.BRANCH_NAME} || true"
				 sh "sudo docker run -d -p 80:80 --name capstnprj1-${env.BRANCH_NAME}  ${dockerHUBUser}/capstnprj1-${env.BRANCH_NAME}"
            }
 
        }
		
		
		stage('DeploytoPROD') { 

            steps {
			
				echo "DeploytoPROD"
                
            }
 
        }
		 
    }           
 }