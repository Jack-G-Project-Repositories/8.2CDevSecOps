pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Jack-G-Project-Repositories/8.2CDevSecOps.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }
        stage('Run Tests') {
            steps {
                bat 'npm test || exit /b 0'
            }
            post
            {
                always
                {
                    emailext
                    (
                        subject: "Jenkins Build - Tests Stage Completed",
                        body: "The Run Tests section has finished, an attached log can be found",
                        to: 'jackgibney3127@gmail.com',
                        attachLog: true
                    )
                }
            }
        }
        stage('Generate Coverage Report') {
            steps {
                bat 'npm run coverage || exit /b 0'
            }
        }
        stage('NPM Audit (Security Scan)') {
            steps {
                bat 'npm audit || exit /b 0'
            }
            post
            {
                always
                {
                    emailext
                    (
                        subject: "Jenkins Build - Security Scan Stage has Completed",
                        body: "The NPM Audit (Security Scan) section has finished, an attached log can be found",
                        attachLog: true
                    )
                }
            }
        }
    }
}