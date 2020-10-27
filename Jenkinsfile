pipeline { 
agent {label 'TestNode' }
	environment
	{
		def buildNumber = env.BUILD_NUMBER
		def branchName = env.BRANCH_NAME
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
			
				sh "docker build -t ${dockerHUBUser}/CapStnPrj1-${branchName}"
                
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