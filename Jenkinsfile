pipeline {
    agent any

    environment {
        LOCAL_INPUTS_PATH = 'D:\\splunk-log-config\\inputs\\inputs.conf'
        SPLUNK_LOCAL_CONF_PATH = 'C:\\Program Files\\Splunk\\etc\\system\\local\\inputs.conf'
    }

    stages {
        stage('Copy inputs.conf from local path') {
            steps {
                bat '''
                echo Checking if inputs.conf exists...
                if exist "%LOCAL_INPUTS_PATH%" (
                    echo inputs.conf found.
                ) else (
                    echo inputs.conf not found. Please verify the file path.
                    exit /b 1
                )

                echo Copying inputs.conf to Splunk local folder...
                xcopy /Y "%LOCAL_INPUTS_PATH%" "%SPLUNK_LOCAL_CONF_PATH%"
                if errorlevel 1 (
                    echo ERROR: Failed to copy inputs.conf!
                    exit /b 1
                )
                '''
            }
        }

        stage('Restart Splunk') {
            steps {
                bat '"C:\\Program Files\\Splunk\\bin\\splunk.exe" restart'
            }
        }
    }
}
