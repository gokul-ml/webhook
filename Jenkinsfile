pipeline {
    agent any
    
    // Injecting our Secret Text globally into a masked environment variable
    environment {
        DB_SECRET = credentials('PROD_DB_PASSWORD')
    }
    
    triggers {
        githubPush() // Listens for your active ngrok/localtunnel webhook
    }
    
    stages {
        stage('Checkout & Verify') {
            steps {
                echo '🚀 Webhook triggered successfully! Pulling latest repository code...'
                sh 'ls -la index.html'
            }
        }
        
        stage('Database Connection Test') {
            steps {
                echo '🗄️ Initializing secure database migration step...'
                // Using double quotes lets Jenkins inject and mask the secret variable safely
                sh "echo 'Connecting to mysql://admin:\$DB_SECRET@prod-database-server:3306/app_db'"
            }
        }
        
        stage('Docker Image Build & Push') {
            steps {
                echo '📦 Packaging application into a Docker container image...'
                sh 'echo "docker build -t gokul/my-web-app:latest ."'
                
                echo '🔑 Fetching secure vault keys to authenticate with DockerHub...'
                // Inline wrapper approach for secure username/password configurations
                withCredentials([usernamePassword(credentialsId: 'DOCKERHUB_REGISTRY_AUTH', 
                                                 usernameVariable: 'DOCKER_USER', 
                                                 passwordVariable: 'DOCKER_PASS')]) {
                    
                    echo "Service Account User: ${DOCKER_USER}"
                    // Simulating a safe corporate registry login and image push execution
                    sh "echo 'Executing: docker login -u ${DOCKER_USER} -p ${DOCKER_PASS}'"
                    sh "echo 'Executing: docker push gokul/my-web-app:latest'"
                }
            }
        }
    }
    
    post {
        always {
            echo '🧹 Cleaning workspace memory tracks...'
            cleanWs()
        }
    }
}
