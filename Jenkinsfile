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
			
				sh "docker build -t ${dockerHUBUser}/capstnprj1-${env.BRANCH_NAME} ."
            }
 
        }
		
		
		stage('TestCode') { 

            steps {
                 
				 echo "TestCode"
            }
 
        }
		
		
		stage('DeploytoPROD') { 

            steps {
			
				echo "DeploytoPROD"
                
            }
 
        }
		 
    }           
 }