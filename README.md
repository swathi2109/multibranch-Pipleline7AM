pipeline {
    agent any

    environment {
        MAVEN_HOME = tool name: 'M3', type: 'ToolLocation'  // Adjust according to your Jenkins Maven installation
        PATH = "${MAVEN_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from GitHub
                git branch: 'main', url: 'https://github.com/swathi2109/multibranch-Pipleline7AM.git'
            }
        }

        stage('Build') {
            steps {
                // Run Maven build
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                // Run unit tests
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                // If you need to deploy, you can add the deploy commands here.
                echo 'Deployment Stage'
            }
        }
    }

    post {
        success {
            echo 'Build successful'
        }
        failure {
            echo 'Build failed'
        }
    }
}
