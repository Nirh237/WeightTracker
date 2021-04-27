pipeline {
    agent {label "slave-ci"}

    stages {
            
        stage('Build') {
            // Creating env file 
            steps {
                    echo 'Building..'
               
            } 
        }
        
    }
   post {
            always {
                    echo 'Creating artifacts'
                    sh 'zip -r my_archive.zip /home/nirh237/workspace/CI'
                    echo 'archiving artifacts'
                    archiveArtifacts artifacts: 'my_archive.zip', onlyIfSuccessful: true
            }
    	}

}







