pipeline { 
agent {label 'TestNode' }
	environment
	{
		def buildNumber = BUILD_NUMBER
		def branchName = BRANCH_NAME
	}
    stages { 
	
        stage('DownloadCode') { 

            steps {
                git url: 'https://github.com/jmunuswa/azure-webapp.git',branch: 'master' 
            }
 
        }
		
		stage('BuildCode') { 

            steps {
			
				sh "docker build -t jmunuswa/CapStnPrj1-${branchName}"
                
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