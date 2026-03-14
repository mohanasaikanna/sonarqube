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
                script {
                   
                    sh "sonar-scanner -Dsonar.login=<sqa_d1501ce4c9ed60e53cfd3ce467ba2bd725289239>"
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
