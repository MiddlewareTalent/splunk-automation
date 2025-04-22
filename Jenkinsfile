pipeline {
    agent any

    environment {
        SPLUNK_PATH = '"C:\\Program Files\\Splunk\\etc\\system\\local"'  // Update this if your Splunk is in another drive

    }

    stages {
        stage('Clone Repo') {
            steps {
                git credentialsId: 'Git', url: 'https://github.com/MiddlewareTalent/splunk-automation.git', branch: 'main'
            }
        }

        stage('Copy inputs.conf') {
            steps {
                bat '''
                echo Copying inputs.conf to Splunk local folder...
                xcopy /Y "%WORKSPACE%\\splunk\\inputs.conf" %SPLUNK_PATH%\\inputs.conf
                if errorlevel 1 (
                    echo ERROR: Failed to copy inputs.conf!
                    exit /b 1
                )
                '''
            }
        }

        stage('Restart Splunk') {
            steps {
                bat '''
                echo Restarting Splunk service...
                "C:\\Program Files\\Splunk\\bin\\splunk.exe" restart
                '''
            }
        }
    }
}
