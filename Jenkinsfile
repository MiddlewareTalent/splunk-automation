pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git credentialsId: 'Git', url: 'https://github.com/MiddlewareTalent/splunk-automation.git', branch: 'main'
            }
        }

        stage('Copy inputs.conf to Splunk') {
            steps {
                bat '''
                echo Copying inputs.conf to Splunk local directory...
                copy inputs\\inputs.conf "C:\\Program Files\\Splunk\\etc\\apps\\search\\local\\inputs.conf" /Y
                '''
            }
        }

        stage('Copy Logs (Optional)') {
            steps {
                bat '''
                echo Copying logs to monitored folder...
                xcopy logs\\* "C:\\sample_logs\\" /Y
                '''
            }
        }

        stage('Restart Splunk') {
            steps {
                bat '''
                echo Restarting Splunk to apply changes...
                "C:\\Program Files\\Splunk\\bin\\splunk.exe" restart
                '''
            }
        }
    }
}
