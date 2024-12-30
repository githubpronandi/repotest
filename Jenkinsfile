pipeline {
    agent any

    environment {
        GITHUB_CREDENTIALS = credentials('github-token') // Use the ID of your secret
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', credentialsId: GITHUB_CREDENTIALS, url: 'https://github.com/your-username/your-repo.git'
            }
        }

        stage('Build') {
            steps {
                sh './gradlew build' // Adjust for your build tool
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                rsync -avz --delete ./build/libs/ /home/redhat/cicd/
                '''
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed!'
        }
    }
}
