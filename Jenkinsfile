pipeline {
    agent any

    environment {
        // Use the credentials ID for your GitHub token (set in Jenkins credentials)
        GITHUB_CREDENTIALS = credentials('github-token')
    }

    stages {
        // Stage 1: Clone the repository
        stage('Clone Repository') {
            steps {
                // Clone the GitHub repository using the GitHub token for authentication
                git branch: 'main', credentialsId: GITHUB_CREDENTIALS, url: 'https://github.com/your-username/your-repo.git'
            }
        }

        // Stage 2: Build the project (Example for a Gradle project)
        stage('Build') {
            steps {
                // Run your build commands. Here we use Gradle as an example
                sh './gradlew build'  // Modify this command according to your project build tool (Maven, npm, etc.)
            }
        }

        // Stage 3: Deploy the build to 192.168.0.128
        stage('Deploy') {
            steps {
                // Use SSH credentials for rsync to the remote server 192.168.0.128
                sshagent (credentials: ['5c30343f-890c-4983-a36c-722f5acaabc8']) {
                    sh '''
                    rsync -avz --delete ./build/libs/ user@192.168.0.128:/home/redhat/cicd/
                    '''
                }
            }
        }
    }

    post {
        // This will run after all stages have finished
        always {
            echo 'Pipeline completed!'
        }
    }
}
