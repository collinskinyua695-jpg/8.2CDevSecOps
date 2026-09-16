pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/collinskinyua695-jpg/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test || true'
            }
        }

        stage('Generate Coverage Report') {
            steps {
                sh 'npm run coverage || true'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                sh 'npm audit || true'
            }
        }

        stage('SonarCloud Analysis') {
            steps {
                withCredentials([string(credentialsId: 'SONAR_TOKEN', variable: 'SONAR_TOKEN')]) {
                    sh '''
                        sonar-scanner \
                          -Dsonar.projectKey=collinskinyua695-jpg_8.2CDevSecOps \
                          -Dsonar.organization=collinskinyua695-jpg \
                          -Dsonar.host.url=https://sonarcloud.io \
                          -Dsonar.token=$SONAR_TOKEN \
                          -Dsonar.sources=. \
                          -Dsonar.exclusions=node_modules/**,test/** \
                          -Dsonar.projectName="NodeJS Goof Vulnerable App" \
                          -Dsonar.sourceEncoding=UTF-8
                    '''
                }
            }
        }
    }
}
