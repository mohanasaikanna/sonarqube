pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/mohanasaikanna/sonarqube.git'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'python3 test.py'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                // Use a Jenkins credential for the token
                withCredentials([string(credentialsId: 'sqa_afccd4f6e58cc2b2538f389086cad6334a766a57', variable: 'TOKEN')]) {
                    sh """
                        sonar-scanner -Dsonar.login=$TOKEN
                    """
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 2, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }

    }
}
