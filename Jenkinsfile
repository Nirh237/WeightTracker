pipeline {
    agent {label "slave-ci"}

    stages {
            
        stage('Build') {
            // Creating env file 
            steps {
                    echo 'Building..'
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
                        
                    }
            }
        }
        
        stage('Deploy') {
           // Running the application 
            steps {
                echo 'Deploying....'
              
                sh 'curl -sL https://deb.nodesource.com/setup_15.x | sudo -E bash -'
                sh 'sudo apt-get install -y nodejs'
                sh 'sudo apt-get install -y build-essential'
                //sh 'cd workspace/CI'
                sh 'npm install'
                sh 'npm run initdb'
                sh 'sudo npm install pm2 -g'                                 // install pm2
                //sh 'pm2 stop src/index.js'
                sh 'pm2 start -f src/index.js'
                sh 'pm2 save'
                //sh 'pm2 start npm -- run dev'                           // run "npm run dev" as a service in the background using pm2
                //sh 'npm run dev'
               
                echo 'Finished building process'
                
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







