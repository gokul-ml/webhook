pipeline {
    agent any
    triggers {
        githubPush() // Tells Jenkins to listen for the GitHub webhook ping
    }
    stages {
        stage('Checkout Code') {
            steps {
                echo '🚀 Webhook received! Pulling newest code from GitHub...'
            }
        }
        stage('Build/Validate') {
            steps {
                echo '🛠️ Validating HTML files...'
                // Simple Windows command to check if our index file exists
                dir index.html
            }
        }
    }
}
