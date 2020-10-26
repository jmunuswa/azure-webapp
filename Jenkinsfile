pipeline { 
agent TestNode 
    stages { 
	
        stage('DownloadCode') { 

            steps {
                git url: 'https://github.com/jmunuswa/azure-webapp.git',branch: 'master' 
            }
 
        }

 
    }           
 }