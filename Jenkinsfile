nirhez
#4945

nirhez — Today at 12:20 PM
הפרויקט הזה שבר אותנו
Genady — Today at 12:21 PM
כן אני רק רוצה להיות ממוקד. עכשיו הצלחתי להעביר איזשהו Pipeline חלקי והוא רק נופל על tar אז יש התקדמות
nirhez — Today at 12:21 PM
:thumbsup_tone2:
Genady — Today at 12:52 PM
Boom

nirhez — Today at 12:52 PM
איזה מלך!
Genady — Today at 12:52 PM
יש TAR. הייתי צריך לשחק עם זה הרבה ולשנות את הקוד. אבל מצד שני עדיף שכתבתי משהו שאני מבין מאשר להסתמך על משהו שנאי לא מבין
nirhez — Today at 12:52 PM
מה עשית?
Genady — Today at 12:52 PM
שיחקתי עם הקוד של tar
ושיניתי מאה אלף פעמים את המיקום
עכשיו יש לנו קובץ tar והוא בתוך ה-slave כפי שאתה רואה
nirhez — Today at 12:53 PM
כל הכבוד
סיימת את שלב הci
Genady — Today at 12:53 PM
אבל הוא נוצר ממש בסוף. אני לא בטוח אם אני אכניס אותו ל-stage של build הוא יווצר כי מקודם זה לא עבד
וזה הרי שלב של CI
ואני הכנסתי את זה לאחרי CD
אנסה להקדים ולבדוק שוב
nirhez — Today at 12:54 PM
לא הבנתי
תשלח לי את הJenkinsfile שלך
אני ניסיתי מקודם ולא הצליח לי
גם משהו עם הtr
Tar
Genady — Today at 12:54 PM
כן אני יושב עליו שעה וחצי
שניה אני עוד משחק
נכשל:

הוא נכשל אם הקובץ נראה ככה:
pipeline {
    agent {label "slave_build"}

    stages {
        
        stage('Downlod_to_BlubStorage') {
Expand
message.txt
3 KB
הסיבה היא משום שהוא מנסה לעשות כיווץ כשהוא לא סיים את ה-stage
nirhez — Today at 12:57 PM
ואיך זה לא נופל?
עזוב את הdeploy עכשיו.
קודם תיצור artifact
אחרי זה ננסה להבין איך לקחת אותו לdeploy
לא חושב?
Genady — Today at 12:58 PM
לא קשור deploy
nirhez — Today at 12:58 PM
איפה הוא בעצם שומר את הartifact?
Genady — Today at 12:58 PM
אני אומר שאתה לא יכול לייצר את הקובץ הזה ב-stage של build והרי אנחנו רוצים כן לייצר אותו שם
תראה בצילום ששלחתי לך
nirhez — Today at 12:58 PM
נכון
Genady — Today at 12:58 PM
הנה הוא:

nirhez — Today at 12:59 PM
אז איך זה כן עבד לך? איך הקוד נראה שזה תקין?
Genady — Today at 1:00 PM
רוצה לדבר בטלפון?
nirhez — Today at 1:01 PM
לא יכול עכשיו אחי
Genady — Today at 1:01 PM
טוב אני שולח לך את הקובץ שכן מצליח tar, אבל רק שים לב שהוא מבצע את זה ממש למטה ולא תחת build
pipeline {
    agent {label "slave_build"}

    stages {
        
        stage('Downlod_to_BlubStorage') {
Expand
message.txt
3 KB
עכשיו בדקתי שוב וזה עובד אבל רק ככה
וככה נראה ה-jenkins

שזה לפחות נראה יפה
Genady — Today at 1:03 PM

nirhez — Today at 1:07 PM
זה גם התקין את כל מה שהרצת שם?
Genady — Today at 1:15 PM
לא זו עדיין בעיה של אתמול מה שאמרנו שנעזוב
זה תחת deploy
﻿
pipeline {
    agent {label "slave_build"}

    stages {
        
        stage('Downlod_to_BlubStorage') {
            steps {
                // TODO - understanding how to do it
                echo 'Downloding Repository from Jenkins to Blub storage'
            }
        }
            
        stage('Build') {
            
            // TODO: Create artifacts
            steps {
                    echo 'Building..'
                    script {
                    
                        // TODO - to be Fixed (must cereate new VM linux)
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
                
        stage('Test') {
            
            steps {
                echo 'Testing..'
            }
        }
        
        stage('Deploy') {
            
            steps {
                echo 'Deploying....'
                
                sh 'curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -'
                sh 'sudo apt-get install -y nodejs'
                sh 'sudo apt-get install -y build-essential'
                sh 'sudo apt install -y npm'
                sh 'npm install'
                sh 'npm run initdb'
                sh 'npm run dev'
                
                echo 'Finished building process'
                
            }
        }
    }

    post {
        always {
            echo 'Creating tar.gz file for artifacts'
            sh 'tar -zcvf /home/nirh237/my_archive.tar.gz /home/nirh237/workspace'
            archiveArtifacts artifacts: 'my_archive.tar.gz', onlyIfSuccessful: true
        }
    }
}
