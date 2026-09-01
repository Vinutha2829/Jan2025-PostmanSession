```groovy
pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo "Building the war"
            }
        }

        stage('Deploy to QA') {
            steps {
                echo "Deploying to QA"
            }
        }

        stage('Checkout') {
            steps {
                git url: 'https://github.com/Vinutha2829/Jan2025-PostmanSession'
            }
        }

        stage('Pull Docker Image') {
            steps {
                bat 'docker pull vinumadhan/gorestapi:1.0'
            }
        }

        stage('Run API Test Cases') {
            steps {
                bat 'docker run -v "%WORKSPACE%\\newman:/app" vinumadhan/gorestapi:1.0'
            }
        }

        stage('Check Newman Reports') {
            steps {
                bat 'echo ===== Newman Report Files ====='
                bat 'dir "%WORKSPACE%\\newman"'
            }
        }

        stage('Publish HTML Extra Report') {
            steps {
                publishHTML([
                    allowMissing: false,
                    alwaysLinkToLastBuild: false,
                    keepAll: true,
                    reportDir: 'newman',
                    reportFiles: '*.html',
                    reportName: 'HTML Extra API Report',
                    reportTitles: ''
                ])
            }
        }

        stage('Deploy to PROD') {
            steps {
                echo "Deploying to PROD"
            }
        }
    }
}
```
