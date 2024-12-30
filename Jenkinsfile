pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/your-username/your-repo.git'
            }
        }

        stage('Build') {
            steps {
                sh './gradlew build' // Adjust based on your build tool
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
