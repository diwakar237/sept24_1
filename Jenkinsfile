pipeline {
    agent any

    parameters {
        booleanParam(name: 'SEND_EMAIL', defaultValue: false, description: 'Check this box to send a notification email upon completion.')
    }

    environment {
        APP_NAME    = 'MyAwesomeApp'
        APP_VERSION = '1.2.0'
    }

    stages {
        // Removed the extra duplicate Checkout stage since Jenkins SCM does this automatically

        stage('Build') {
            steps {
                echo "Compiling application: ${env.APP_NAME} v${env.APP_VERSION}"
                echo "Simulating compilation of app.py... Done!"
            }
        }

        stage('Send Notification') {
            when {
                expression { params.SEND_EMAIL == true }
            }
            steps {
                // Safe echo workaround to avoid SMTP connection errors
                echo "Simulating sent email to: diwakar.s2024a@vitstudent.ac.in"
                echo "Subject: Build Alert: ${env.APP_NAME} - Version ${env.APP_VERSION}"
                echo "Body: The build for ${env.APP_NAME} version ${env.APP_VERSION} has completed successfully."
            }
        }
    }
}
