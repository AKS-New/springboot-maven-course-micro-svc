pipeline {
    agent any

    stages {
        stage("Sonar Quality Check") {
            // No need to use 'steps' in Scripted Pipeline
            script {
                withSonarQubeEnv(installationName: 'sonarqube', credentialsId: 'sonarqube') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
        
        stage("SonarQube Quality Gate") {
            script {
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}

