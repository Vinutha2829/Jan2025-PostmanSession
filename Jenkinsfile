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
            bat '''
                if exist "%WORKSPACE%\\newman" rmdir /s /q "%WORKSPACE%\\newman"
                mkdir "%WORKSPACE%\\newman"

                docker run --name gorest-container vinumadhan/gorestapi:1.0

                docker cp gorest-container:/app/. "%WORKSPACE%\\newman\\"

                docker rm gorest-container
            '''
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
