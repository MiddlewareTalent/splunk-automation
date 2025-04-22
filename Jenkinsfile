pipeline {
    agent any

    environment {
        SPLUNK_PATH = '"C:\\Program Files\\Splunk"'
        INPUTS_CONF_SOURCE = 'inputs\\inputs.conf'
        INPUTS_CONF_DEST = 'C:\\Program Files\\Splunk\\etc\\system\\local\\inputs.conf'
    }

    stages {
        stage('Pull From GitHub') {
            steps {
                git branch: 'main', url: 'https://github.com/your-repo/splunk-log-config.git'
            }
        }

        stage('Copy inputs.conf to Splunk') {
            steps {
                bat "copy ${INPUTS_CONF_SOURCE} \"${INPUTS_CONF_DEST}\" /Y"
            }
        }

        stage('Restart Splunk') {
            steps {
                bat "\"${SPLUNK_PATH}\\bin\\splunk.exe\" restart"
            }
        }
    }
}
