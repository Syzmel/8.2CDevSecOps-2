pipeline {
    agent any
        environment {
        PATH = "C:\\Program Files\\nodejs;${env.PATH}"
        //SONAR_TOKEN = credentials('ae3e0cd85e60d4e43416a9ebf03d827702acd046')
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Syzmel/8.2CDevSecOps.git'
            }
        }
        stage('Install Dependencies') {
            steps {
               bat 'npm install'
            }
        }
        stage('Run Tests') {
            steps {
                bat 'npm test || exit /B 0'
            }
        }
        stage('Generate Coverage Report') {
            steps {
                bat 'npm run coverage || exit /B 0'
            }
        }
        stage('NPM Audit (Security Scan)') {
            steps {
                bat 'npm audit || exit /B 0'
            }
        }
        stage('SonarCloud Analysis') {
            steps {
                                bat '''
                  sonar-scanner ^
                  -Dsonar.projectKey=8-2cdevsecops-2 ^
                  -Dsonar.organization=8.2CDevSecOps-2 ^
                  -Dsonar.sources=. ^
                  -Dsonar.host.url=https://sonarcloud.io ^
                  -Dsonar.login=ae3e0cd85e60d4e43416a9ebf03d827702acd046
                  if %ERRORLEVEL% NEQ 0 exit /b 0
                '''

            }
        }  
    }
}
