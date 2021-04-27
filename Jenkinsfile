pipeline {
    agent {label "slave-ci"}

    stages {
            
        stage('Build') {
            // Creating env file 
            steps {
                    echo 'Building..'
                /*
                    script {
                   
                        echo 'creating .env file'
                        sh '''
                     
                        
                        echo "# Host configuration
                        PORT=8080
                        HOST=0.0.0.0
                        NODE_ENV=development
                        HOST_URL=Http://20.86.114.177:8080
               	        COOKIE_ENCRYPT_PWD=superAwesomePasswordStringThatIsAtLeast32CharactersLong!
                        # Okta configuration
                        OKTA_ORG_URL=https://dev-72046139.okta.com
                        OKTA_CLIENT_ID=0oan7xtk2lsVGQ9h25d6
                        OKTA_CLIENT_SECRET=KqbrK832bsa4RIWuFUpnqtQb8zuLkPq-6D4kDFEZ
                        # Postgres configuration
                        PGHOST=10.0.1.4
                        PGUSERNAME=postgres
                        PGDATABASE=postgres
                        PGPASSWORD=password
                        PGPORT=5432" > .env
                        '''
                        
                    }*/
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







