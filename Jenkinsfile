pipeline {
    agent any

    // Define the boolean parameter for the user checkbox
    parameters {
        booleanParam(name: 'SEND_EMAIL', defaultValue: false, description: 'Check this box to send a notification email upon completion.')
    }

    // Custom environment block defining application metadata
    environment {
        APP_NAME    = 'MyAwesomeApp'
        APP_VERSION = '1.2.0'
    }

    stages {
        stage('Checkout') {
            steps {
                // This command tells Jenkins to clone the specific GitHub repository configured in the UI
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Echoes the custom environment block variables
                echo "Compiling application: ${env.APP_NAME} v${env.APP_VERSION}"
                
                // If you added an app.py file to your repo, use: sh 'python3 -m py_compile app.py'
                // Otherwise, this echo statement acts as a safe placeholder:
                echo "Simulating compilation of app.py... Done!"
            }
        }

        stage('Send Notification') {
            // Controlled by a when directive checking the booleanParam
            when {
                expression { params.SEND_EMAIL == true }
            }
            steps {
                echo "Sending email notification for ${env.APP_NAME} version ${env.APP_VERSION}..."
                
                // Standard Jenkins mail step implementation
                mail to: 'team@example.com',
                     subject: "Build Alert: ${env.APP_NAME} - Version ${env.APP_VERSION}",
                     body: "The build for ${env.APP_NAME} version ${env.APP_VERSION} has completed successfully."
            }
        }
    }
}
