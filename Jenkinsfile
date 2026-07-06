pipeline {
    agent any
    triggers {
        githubPush() // Listens for your working GitHub webhook trigger
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
                // 'sh' executes native Linux commands inside your Jenkins container
                sh 'ls -la index.html' 
            }
        }
    }
}
