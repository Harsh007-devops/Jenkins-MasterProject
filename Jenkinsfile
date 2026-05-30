pipeline {

    agent any

    tools {
        maven 'mymaven'
        
    }

    options {
        buildDiscarder(logRotator(numToKeepStr: '10'))
        timestamps()
        disableConcurrentBuilds()
    }

    environment {
        APP_NAME = "java-demo-app"
        BUILD_VERSION = "${BUILD_NUMBER}"
    }

    stages {

        stage('Checkout Source Code') {
            steps {
                echo "Checking out source code from GitHub..."
                git branch: 'main',
                url: 'https://github.com/Harsh007-devops/Jenkins-MasterProject.git'
            }
        }

        stage('Build Application') {
            steps {
                echo "Compiling Java application..."
                sh 'mvn clean compile'
            }
        }

        stage('Run Tests') {
            steps {
                echo "Executing test cases..."
                sh 'mvn test'
            }
        }

        stage('Package Application') {
            steps {
                echo "Packaging application..."
                sh 'mvn package -DskipTests'

                archiveArtifacts artifacts: 'target/*.jar',
                                 fingerprint: true
            }
        }
    }

    post {

        success {
            echo "Pipeline executed successfully."
            echo "Artifact generated and archived."
        }

        failure {
            echo "Pipeline failed. Check console logs."
        }

        always {
            cleanWs()
        }
    }
}
