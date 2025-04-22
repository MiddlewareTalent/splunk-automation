pipeline {
    agent any

    environment {
        SPLUNK_PATH = '"C:\\Program Files\\Splunk\\etc\\system\\local"'  // Change if Splunk is installed elsewhere
    }

    stages {
        stage('Clone Repo') {
            steps {
                git credentialsId: 'Git', url: 'https://github.com/MiddlewareTalent/splunk-automation.git', branch: 'main'
            }
        }

        stage('Check Directory') {
            steps {
                bat 'dir "%WORKSPACE%\\splunk-log-config\\inputs"'
            }
        }

        stage('Copy inputs.conf') {
            steps {
                bat '''
                echo Checking if inputs.conf exists...
                if exist "%WORKSPACE%\\splunk-log-config\\inputs\\inputs.conf" (
                    echo inputs.conf found.
                ) else (
                    echo inputs.conf not found. Please verify the file path.
                    exit /b 1
                )

                echo Copying inputs.conf to Splunk local folder...
                xcopy /Y "%WORKSPACE%\\splunk-log-config\\inputs\\inputs.conf" "C:\\Program Files\\Splunk\\etc\\system\\local\\inputs.conf"
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
