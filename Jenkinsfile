pipeline {
    agent {label "slave"}

    stages {
        stage('Downlod_to_BlubStorage') {
            steps {
                // TODO - understanding how to save
                echo 'Downloding to Blub storage'
            }
        }
        stage('Build') {
            steps {

                echo 'creating .env file'

                sh '''
                echo "# Host configuration
                PORT=8080
                HOST=0.0.0.0
                NODE_ENV=development
                HOST_URL=Http://20.86.121.99:8080
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

                echo 'Building..'

                sh 'sudo apt-get install -y nodejs'
                sh 'sudo apt install -y npm'
                sh 'npm install'
                sh 'npm run initdb'
                sh 'npm run dev'

                echo 'Finished building process'

            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
