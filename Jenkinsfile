pipeline {
    agent{
        label 'slave1'
    }

    tools {
        maven 'Maven 3.8.5' // Ensure this matches the Maven version configured in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from the repository
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Run Maven build to compile the code and create an artifact
                sh 'mvn clean package'
            }
        }

        stage('Archive') {
            steps {
                // Archive the generated JAR file
                archiveArtifacts artifacts: 'target/*.jar', allowEmptyArchive: true
            }
        }
    }

    post {
        always {
            // Clean up the workspace after the build
            cleanWs()
        }

        success {
            echo 'Build and artifact creation successful!'
        }

        failure {
            echo 'Build failed!'
        }
    }
}
